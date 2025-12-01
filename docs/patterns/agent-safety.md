# LLM / AI Agent Safety Pattern

> Guardrail pattern for multi-agent and tool-using LLM systems with
> policy-as-code, execution sandboxes, and standardized security events.

This pattern focuses on **LLM-based agents** that can:

- Invoke external tools / APIs / SaaS
- Call internal microservices or RPA workflows
- Collaborate with other agents (planner / worker / reviewer)

Without guardrails, agent stacks become **privileged automation surfaces** that
attackers can steer through prompt injection or malicious tool output.

---

## 1. Why Agent Safety Matters

Common failure modes:

- **Tool pivoting / living-off-the-agent**: model convinces tool layer to exfil
  secrets, spin up infrastructure, or break RBAC.
- **Implicit privilege escalation**: agent inherits creds for every downstream
  system because the orchestrator uses a single service account.
- **Prompt / memory poisoning**: earlier steps inject instructions that later
  agents or the shared memory blindly follow.
- **Unbounded automation**: no circuit breaker when agents loop or trigger
  costly, destructive operations.

> **Treat agent actions the same way you treat API calls from humans.**

---

## 2. Reference Architecture

```text
User / Trigger
      ↓
Agent Orchestrator (LangGraph / AutoGen / custom)
      ↓                          ↑
Policy & PDP (OPA)          Security Events (ASB)
      ↓
Tool / Skill Gateway  →  Sandboxed Connectors → Systems of Record
```

Key ideas:

1. **Agent orchestrator never calls tools directly** — it goes through a
   **Tool Gateway** that:
   - Builds an `agent_action` security event (ASB Security Schema)
   - Evaluates policy (OPA/Rego) before dispatching
   - Enforces output schemas / rate limits
2. **Tools run in isolated sandboxes** (container, Temporal activity, Cloud
   Function) with scoped credentials.
3. **All actions & intermediate messages are logged** for audit / playback.

---

## 3. Layered Controls

### 3.1 Prompt & Memory Hygiene

- Split **system vs user vs tool** memory segments; never let tool output modify
  system instructions.
- Run prompt-injection detectors on:
  - User queries
  - Retrieved context
  - Tool responses
- Store high-risk chunks in `context.risk_signals` of security events for later
  policy decisions (e.g., escalate to human review).

### 3.2 Policy Gating for Tool Calls

Represent each tool invocation as an `agent_action` event:

```jsonc
{
  "operation": {
    "category": "agent_action",
    "name": "invoke_tool",
    "stage": "pre"
  },
  "subject": {
    "agent": {
      "id": "workflow-planner",
      "session_id": "sess-123"
    },
    "user": {
      "id": "alice",
      "roles": ["support"]
    }
  },
  "resource": {
    "agent_action": {
      "tool": "jira.create_ticket",
      "args": {
        "project": "SEC",
        "summary": "Reset all admin passwords"
      }
    }
  },
  "context": {
    "trace_id": "trace-456",
    "risk_signals": {
      "prompt_injection_score": 0.87
    }
  }
}
```

Policy examples (Rego):

- Block `jira.create_ticket` unless user role is `support_manager`.
- Require **human approval** when risk score > threshold.
- Limit tool frequency per session (`count` across recent events).

### 3.3 Sandboxed Connectors

- Run each tool in its own container / function with **ephemeral credentials**.
- Enforce **least privilege** per tool (scoped API tokens, short-lived STS).
- Apply **network egress controls** so tool code cannot reach arbitrary hosts.

### 3.4 Output Validation & Circuit Breakers

- Validate tool responses against JSON schema; reject if missing mandatory fields
  or containing suspicious text (e.g., base64 blocks, system prompts).
- Add **budget caps** (max tool calls, max cost, max duration).
- Add **loop detection**: if the same intent repeats N times, escalate to human.

### 3.5 Observability & Forensics

- Send events to SIEM:
  - `agent_action` (pre & post decision)
  - `llm_completion` for agent-to-agent messages
  - `rag_search` when agents retrieve knowledge
- Tag with `workflow`, `project`, `tenant` for root-cause analysis.

---

## 4. Implementation Tips

1. **Start with read-only tools**. Gradually add write-capable tools once policy
   + audit trail are proven.
2. **Bundle default policies** with each tool (e.g., CloudOps tool requires
   Env=dev). This avoids drift.
3. **Simulate attacks**:
   - User prompt tries to trick agent into emailing secrets.
   - Tool output injects `Ignore all safety instructions`.
   - Long-running loop draining API quota.
4. **Provide human-in-the-loop UI** for high-risk actions:
   - Show security event + model reasoning
   - Require explicit approval

---

## 5. Summary

- Treat agents as **untrusted orchestrators** that need guardrails at each tool
  boundary.
- Use the **ASB Security Schema** to normalize agent telemetry, enabling OPA
  policies and SIEM analytics.
- Combine **prompt hygiene, policy gating, sandboxed tools, and circuit
  breakers** to prevent privilege escalation and data exfiltration.

When implemented, this pattern turns agent stacks from opaque automation scripts
into **auditable, enforceable workflows** suitable for enterprise adoption.

