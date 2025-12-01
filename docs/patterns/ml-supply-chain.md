# ML Supply Chain Security Pattern

> Pattern for securing data, code, dependencies, and model artifacts across the
> ML lifecycle with provenance, attestations, and continuous verification.

Traditional software supply chain controls (SBOMs, SLSA, artifact signing) must
be extended to cover **datasets, notebooks, pipelines, and third-party models**.

---

## 1. Attack Surfaces

- **Dataset poisoning** via public contributions / data brokers.
- **Compromised training pipelines** (malicious notebook, CI runner).
- **Unvetted open-source models** embedded into products.
- **Dependency drift** (CUDA, PyTorch wheels) introducing CVEs or backdoors.
- **Artifact swapping** between training and deployment.

> The ML supply chain is more than code — it includes *data lineage, weights,
> hyperparameters, and evaluation evidence*.

---

## 2. Supply Chain Map

```text
Data Sources → Feature Store → Training Pipelines → Model Registry → Deployment
    |               |                 |                  |                |
 Data Contracts   Data SBOM      Build Attestations   Model Cards     Runtime Attest
```

Each stage should emit structured events (ASB) and produce verifiable metadata.

---

## 3. Controls by Stage

### 3.1 Data Acquisition & Feature Stores

- **Data contracts**: declare schema, allowed values, retention, owners.
- Compute **data SBOM**:
  - Source URL / bucket
  - License / consent flag
  - PII classification level
- Run **poisoning detectors** (outlier detection, duplication heuristics).
- Emit `dataset_ingest` event capturing source, hashes, and reviewer.

### 3.2 Training Code & Dependencies

- Enforce Infra-as-Code for pipelines (Terraform, Argo, Airflow) with reviews.
- Pin versions for:
  - Frameworks (PyTorch, TensorFlow)
  - CUDA / cuDNN
  - Base OS images
- Scan notebooks / scripts for secrets, network calls, unsafe shell usage.
- Use **signed container images** for training jobs; deny unsigned workloads.

### 3.3 Model Registry & Governance

- Store every model with:
  - Lineage metadata (`dataset_ids`, `code_commit`, `training_run_id`)
  - Evaluation metrics + test datasets
  - Risk assessment (bias, safety, robustness)
- Require **two-person review** or automated gates before promoting to “deployable”.
- Sign registry entries and generate **Model SBOM** referencing datasets +
  dependencies.

### 3.4 Third-party / OSS Models

- Treat them like binaries:
  - Verify publisher signature or download hash.
  - Review license + usage rights.
  - Run sandboxed evaluation (safety, prompt injection susceptibility).
- Record provenance in `model_release` event with `source = "third_party"`.

### 3.5 Deployment & Runtime

- Enforce that only **approved registry digests** can be deployed (see Model
  Deployment pattern).
- Continuously verify runtime weights (hash comparison, remote attestation).
- Monitor for **drift from declared lineage**: if a deployment references a
  dataset not in the SBOM, raise alert.

---

## 4. Policy & Telemetry (ASB Schema)

Use ASB events to stitch lineage:

- `dataset_ingest` → `training_run` → `model_release` → `deployment` →
  `inference_request`
- Each event includes `precedence_id` / `parent_id` fields to form a graph.

Example policy (Rego):

```rego
package asb.model_release

default allow = false

allow {
  input.operation.category == "model_release"
  not forbidden_dataset
  input.resource.model_release.attestations[_] == "bias-eval-pass"
}

forbidden_dataset {
  some ds
  ds := input.resource.model_release.datasets[_]
  ds.license == "unknown"
}
```

This blocks publishing models trained on unlicensed data.

---

## 5. Continuous Verification

1. **Nightly lineage audit**:
   - Query data lake for models lacking complete SBOM or attestations.
2. **Runtime scanner**:
   - Compare running checksum vs registry digest.
   - Validate GPU driver version against approved list.
3. **Incident drills**:
   - Revoke a dataset and ensure dependent models are quarantined automatically.

---

## 6. Implementation Tips

- Reuse existing tools (Snyk, Grype, Trivy, Sigstore) for container + dependency
  scanning; wrap ML-specific metadata around them.
- Automate SBOM generation via scripts that inspect training config files and
  dataset manifests.
- Keep **human-readable model cards** alongside machine-readable metadata so
  reviewers understand risk.
- Integrate supply-chain status into PR / MR templates (checklist: data license,
  evaluation results, attestation links).

---

## 7. Summary

- Extend supply-chain practices to cover **data, training code, and models**.
- Generate **verifiable metadata** (SBOMs, attestations, ASB events) at every
  stage, enabling policy enforcement and auditing.
- Continuously verify runtime against declared lineage to detect tampering or
  unapproved assets.

Following this pattern keeps ML systems compliant and resilient against
poisoning, dependency compromises, and artifact swaps.

