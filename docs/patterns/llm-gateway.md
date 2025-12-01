# LLM Gateway Guardrail Pattern

> Deploy an API gateway in front of LLM services to enforce authn/z, content
> filtering, policy-as-code, and ASB-standard telemetry for every prompt +
> completion.

This pattern applies whether you host an open-source model, call a SaaS API, or
proxy many providers. The **gateway** becomes the control plane for safety,
compliance, and cost management.

---

## 1. Why an LLM Gateway?

- Central place to enforce **authentication, quotas, budgets**.
- Consistent **prompt/response filtering** regardless of provider.
- Observability + audit trail (`prompt_submission`, `llm_completion` events).
- Ability to route / failover across models without app changes.

Without a gateway, each app re-implements controls (inconsistently) and you
cannot answer “Who sent this prompt?” or “Which response leaked data?”.

---

## 2. Reference Flow

```text
Client / App
   |
   v
LLM Gateway
   |   ↘ Policy Decision (OPA) + ASB events
   v
Provider Adapters (OpenAI, Anthropic, OSS hosters)
```

---

## 3. Core Capabilities

### 3.1 Authentication & Authorization

- Support API keys, OAuth2 client credentials, or mTLS.
- Map tokens to **tenants / projects / roles**.
- Enforce RBAC/ABAC:
  - Which models a tenant can access
  - Max context length / cost per request

### 3.2 Prompt & Response Filtering

1. **Pre-processing**
   - Sanitize structured inputs (JSON schema validation).
   - Run detectors for PII, secrets, malware intent.
   - Tag results as `context.risk_signals` → OPA can escalate/deny.
2. **Post-processing**
   - Inspect completions for policy violations (toxic, data leakage).
   - Mask or reject responses; attach `decision.effect`.

### 3.3 Routing & Failover

- Policy-driven routing:
  - `if tenant == finance -> use internal model`
  - `if request contains PHI -> route to HIPAA-compliant provider`
- Weighted or fallback routing when providers throttle / fail.

### 3.4 Quotas & Cost Controls

- Track tokens / dollars per tenant, per time window.
- Hard/soft limits with alerting.
- Optionally inject optimization (cache previous completion, apply compression).

---

## 4. Telemetry (ASB Security Schema)

Emit structured events for each stage:

1. `prompt_submission` (pre-decision)

```jsonc
{
  "operation": {"category": "prompt_submission", "stage": "pre"},
  "subject": {"user": {"id": "alice", "tenant": "acme"}},
  "resource": {
    "prompt": {
      "model": "gpt-4o",
      "input": {"messages": [{"role": "user", "content": "Show SSNs"}]},
      "metadata": {"app_id": "kb-bot"}
    }
  },
  "context": {"risk_signals": {"pii_detected": true}}
}
```

2. Policy engine returns allow/deny/mask.

3. `llm_completion` (post-decision) captures provider response, tokens, latency,
   and `decision`.

Benefits:

- Unified audit logs across providers.
- SIEM dashboards for risky prompts/responses.
- Forensics: link completions back to user + tenant + app.

---

## 5. Policy as Code Examples

### Deny requests with unapproved model IDs

```rego
package asb.prompt

default allow = false

allow {
  input.operation.category == "prompt_submission"
  allowed_models := {"gpt-4o", "internal-qa-v2"}
  allowed_models[input.resource.prompt.model]
}
```

### Require human review for high-risk completions

```rego
package asb.llm_completion

default decision = {"effect": "allow"}

decision = {"effect": "review", "reason": "pii"} {
  input.context.risk_signals.pii_detected == true
}
```

Gateway pipeline:

1. Build ASB event → send to OPA.
2. Apply decision (block, mask, review).
3. Log final event with decision metadata.

---

## 6. Implementation Tips

- **Modular adapters**: wrap each provider with a standard interface, enabling
  retries, tracing, and provider-specific auth.
- **Caching**: optionally memoize deterministic prompts to cut cost—store cache
  keys + hits in events for transparency.
- **Developer ergonomics**: provide SDKs/clients so product teams don’t bypass
  the gateway.
- **Health monitoring**: track provider latency/error rate; auto-brownout when
  they breach SLOs.
- **Secrets handling**: gateway stores provider credentials; clients never see
  them.

---

## 7. Summary

- An LLM gateway centralizes **safety, compliance, and routing** for all
  generative workloads.
- Pair it with **ASB security events + OPA** to make every prompt auditable and
  enforceable.
- Add value with **quota management, multi-provider routing, and filtering** so
  application teams focus on business logic, not duplicating guardrails.

