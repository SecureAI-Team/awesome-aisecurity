# Model Deployment Hardening Pattern

> Secure pattern for packaging, signing, and operating ML/LLM inference
> services with zero-trust controls and ASB-aligned telemetry.

Once a model is trained, deployment pipelines often shortcut traditional AppSec
steps. This pattern ensures **model artifacts, serving stacks, and inference
APIs** get the same rigor as production microservices.

---

## 1. Threats in Model Deployment

- **Unsigned / tampered artifacts** inserted between training and serving.
- **Insecure serving images** (outdated CUDA, unauthenticated endpoints).
- **Cross-tenant data leakage** via shared GPU memory or caching layers.
- **Model extraction** by unthrottled inference scraping.
- **Lack of observability**: no traceability from prediction back to model
  version or training data.

---

## 2. Architecture Checklist

```text
Registry          CI/CD            Serving Platform
  |                 |                     |
Model Card ─→ Signing / SBOM ─→ Image Registry ─→ Serving Cluster
  |                 |                     |
ASB Events (model_release, inference_request, llm_completion, etc.)
```

Controls span three phases: **package**, **deploy**, **operate**.

---

## 3. Phase 1 – Package & Sign

### 3.1 Deterministic Packaging

- Use reproducible build scripts (Bazel, Docker multi-stage) to bundle:
  - Model weights
  - Tokenizer / vocab
  - Runtime dependencies
- Generate **SBOM + manifest** describing hashes, licenses, CUDA versions.

### 3.2 Artifact Signing & Attestation

- Sign model artifacts using Sigstore / Cosign or internal KMS.
- Emit a `model_release` security event containing:

```jsonc
{
  "operation": {"category": "model_release", "name": "publish"},
  "resource": {
    "model_release": {
      "model_id": "kb-qa-001",
      "version": "2025.03.15",
      "artifact_digest": "sha256:...",
      "sbom_uri": "s3://ml-artifacts/qa-001/bom.json",
      "attestations": ["slsa-level2", "vuln-scan-clean"]
    }
  }
}
```

Policies can block deployments when attestations are missing.

---

## 4. Phase 2 – Deploy & Serve

### 4.1 Harden Serving Images

- Base on minimal OS (Distroless / Wolfi).
- Remove compilers, curl, unnecessary shells.
- Apply **GPU isolation** (MIG, gVisor, Kata) for multi-tenant clusters.
- Enforce TLS mutual auth between gateway ↔ serving pods.

### 4.2 Zero-Trust Inference Gateway

- All inference APIs sit behind an **LLM/Model Gateway** that:
  - Authenticates/authorizes clients (per-tenant API keys or OIDC)
  - Throttles requests & enforces rate limits
  - Logs each call as `inference_request` event with model ID, version, tenant
  - Optionally handles content filters (see LLM Gateway pattern)

### 4.3 Runtime Policy Enforcement

- Use OPA/Envoy to ensure only approved model versions run in each environment.
- Example policy: deny pods whose `model_version` label lacks approved attestation.

---

## 5. Phase 3 – Operate & Observe

### 5.1 Telemetry

- Emit ASB events for:
  - `inference_request` (pre/post) – includes subject, payload metadata, model
  - `llm_completion` – for generative outputs
  - `model_health` – custom event for drift, anomaly scores
- Export metrics: latency, token counts, GPU utilization, error codes.

### 5.2 Guarding Against Abuse

- Apply **per-tenant quotas** (requests, tokens, cost).
- Detect **model extraction** via:
  - Sudden spikes in near-identical prompts
  - Crawling patterns (alphabetical queries, high entropy)
- Support **kill switch**: ability to revoke a compromised model version across
  clusters (automated rollback + policy update).

### 5.3 Incident Response Hooks

- Link inference events to training lineage: `model_release.parent_run_id`.
- Keep  audit-ready logs for “Who knew this version was deployed?”
- Define runbooks for:
  - CVE in serving image → patch + redeploy
  - Hallucination impacting customers → freeze version, replay logs

---

## 6. Implementation Tips

1. **Integrate with DevSecOps**: reuse container scanning, IaC scanning, and
   artifact signing pipelines instead of bespoke ML tooling.
2. **Automate promotion gates** (dev → staging → prod) based on evaluation
   metrics + security attestations.
3. **Continuously verify**: schedule CronJobs that hash running weights and
   compare with registry digests.
4. **Document assumptions** in a model card section: threat model, dependency
   lists, required environment variables.

---

## 7. Summary

- Treat model artifacts as **software releases** with SBOMs, signatures, and
  policy gates.
- Place a **gateway** in front of all inference traffic to authenticate, audit,
  and throttle usage.
- Stream **ASB-aligned telemetry** so every prediction can be traced to a model
  version, deployment, and training lineage.

With these controls, model deployments move from ad-hoc scripts to **auditable,
zero-trust services** suitable for production workloads.

