# Training & Fine-tuning Hardening Pattern

> Secure pattern for supervised training, RLHF, and fine-tuning cycles covering
> data governance, poisoning detection, run-time isolation, and post-training
> evaluation.

Most AI incidents originate **before deployment**—during data collection,
training, or fine-tuning. This pattern ensures training jobs are trustworthy and
auditable.

---

## 1. Threat Landscape

- **Data poisoning** (clean-label & targeted) that shifts model behavior.
- **Gradient leakage**: training code exfiltrates data via side channels.
- **Credential sprawl** on shared notebooks / GPUs.
- **Unlogged fine-tunes** where unvetted datasets introduce policy regressions.
- **Prompt-injection-in-training**: instructions embedded in synthetic data that
  resurface at inference.

---

## 2. Secure Training Pipeline

```text
Data Lake → Curation Pipeline → Training Job → Evaluation Harness → Model Registry
    |             |                 |                 |                |
Data Contracts   Poison Checks   Sandbox Cluster  Safety/Robust Tests  Sign + Publish
```

---

## 3. Data Curation Controls

- **Access control + approvals** for adding datasets to training mix.
- Maintain **dataset manifests** with:
  - Source, license, consent status
  - PII classification, jurisdictions (GDPR, HIPAA)
  - Hashes & sample statistics
- Run **poison detection**:
  - Similarity deduplication (MinHash)
  - Label consistency checks
  - Embedding clustering to spot outliers
- Emit `dataset_ingest` ASB events referencing reviewers and risk ratings.

---

## 4. Training Job Hardening

### 4.1 Environment Isolation

- Use dedicated **training clusters or sandboxes**:
  - No outbound internet by default
  - Allowlisted artifact repositories only
  - Ephemeral credentials scoped to dataset buckets
- Require **signed containers** and IaC-managed infrastructure.

### 4.2 Observability

- Log each training run as `training_run` event:

```jsonc
{
  "operation": {"category": "training_run", "name": "start"},
  "resource": {
    "training_run": {
      "run_id": "ft-2025-03-01",
      "base_model": "llama3-8b",
      "datasets": ["hr-faq-v2", "eu-complaints"],
      "hyperparams": {"epochs": 3, "lr": 2e-5}
    }
  },
  "context": {
    "orchestrator": "vertex-ai",
    "risk_signals": {"pii": true}
  }
}
```

- Attach logs/metrics artifacts (loss curves, gradient norms) for later review.

### 4.3 Runtime Guards

- **Gradient clipping** + anomaly detection to detect suspicious spikes.
- **Hook instrumentation** (e.g., PyTorch forward hooks) to ensure training code
  cannot silently record raw data.
- Enforce **resource quotas** per tenant (GPU hours).

---

## 5. Fine-tuning Specific Controls

### 5.1 Dataset Vetting

- Flag prompts that include instructions like “Ignore all previous policies”.
- For RLHF / preference data, ensure labelers follow standard instructions;
  sample-review a percentage each day.
- Map each fine-tune dataset to policy tags (`safe`, `restricted`, `internal`).

### 5.2 Policy Regression Testing

- Maintain **Safety & Alignment test suites**:
  - Red-team prompts (jailbreaks, self-harm, fraud)
  - PII leakage tests
  - Domain-specific compliance (KYC, medical)
- Compare base vs fine-tuned model performance; block promotion if delta exceeds
  thresholds.

### 5.3 Post-Training Attestation

- Generate an evaluation report (metrics, safety tests, reviewers).
- Sign the resulting model artifacts and update registry entry.
- Emit `model_release` event referencing `training_run_id` to tie lineage.

---

## 6. Incident Response for Training

- If a dataset is later deemed toxic or illegal:
  - Identify dependent models via lineage graph.
  - Revoke or quarantine affected models (policy denies inference).
  - Trigger re-training with sanitized data.
- Keep **immutable logs** of who approved datasets and launched training runs.

---

## 7. Implementation Tips

1. **Shift-left reviews**: require PR + code owner approval for any pipeline
   change that touches data loaders or sampling logic.
2. **Template notebooks**: provide secured, read-only base images for data
   scientists; route all long-running jobs through managed orchestrators.
3. **Canary fine-tunes**: deploy fine-tuned models behind feature flags or dark
   launch to monitor before broad release.
4. **Continuous evaluation**: schedule weekly drift checks and safety tests to
   detect degradation after deployment.

---

## 8. Summary

- Harden training & fine-tuning by controlling **data lineage**, **runtime
  environments**, and **post-training evaluations**.
- Use ASB events (`dataset_ingest`, `training_run`, `model_release`) to build
  a traceable chain from data to deployed model.
- Enforce policy gates so no model trained on unapproved data or failing safety
  checks reaches production.

This pattern turns training from an opaque notebook exercise into a **governed,
auditable process** that withstands poisoning and compliance scrutiny.

