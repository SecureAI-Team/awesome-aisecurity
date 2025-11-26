# Awesome AI Security

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

A curated list of **awesome resources for securing AI systems** – including open-source libraries, academic papers, standards, frameworks, datasets, and real-world case studies.

> Focus: **Security of AI systems** (models, data, pipelines, infrastructure), not *AI for cybersecurity applications*.

[中文说明 / Chinese README](./README_zh.md)

---

## Contents

- [Motivation & Scope](#motivation--scope)
- [Foundations & Learning Resources](#foundations--learning-resources)
- [Threat Modeling & Frameworks](#threat-modeling--frameworks)
- [Adversarial Machine Learning](#adversarial-machine-learning)
- [LLM & GenAI Security](#llm--genai-security)
- [Privacy, Safety & Governance](#privacy-safety--governance)
- [Supply Chain & MLOps Security](#supply-chain--mlops-security)
- [Infrastructure & Runtime Security](#infrastructure--runtime-security)
- [Datasets & Benchmarks](#datasets--benchmarks)
- [Industrial & Domain-specific AI Security](#industrial--domain-specific-ai-security)
- [Related Awesome Lists & External Resources](#related-awesome-lists--external-resources)
- [Contributing](#contributing)
- [License](#license)

---

## Motivation & Scope

Modern AI systems (from classical ML to large foundation models) introduce new attack surfaces across **data, models, pipelines, infrastructure, and governance**.

This repository aims to:

- Provide a **curated map** of the AI security landscape.
- Help practitioners quickly find **reliable tools, papers, and frameworks**.
- Bridge the gap between **academic research** and **real-world engineering practice**.

**In scope**

- Security, robustness, and trustworthiness **of AI systems**:
  - Adversarial ML, LLM & GenAI security.
  - Data poisoning, model stealing, backdoors.
  - Privacy attacks & defenses.
  - AI supply chain and MLOps security.
  - Runtime / infra security for model serving.
  - AI governance & risk management.

**Out of scope (linked instead of duplicated)**

- General cybersecurity that does not specifically involve AI.
- “AI for security” (e.g., IDS using ML) – we link to other lists where appropriate.

_Last update: 2025-11-26 (keep this up to date manually)_

---

## Foundations & Learning Resources

> Books, tutorials, surveys, and entry points into AI security.

- **Books & Surveys**
  - *TODO:* `- **Title of Book / Survey** (Year) - One-line description. [Link](https://example.com)`
- **Tutorials & Courses**
  - *TODO:* `- [Course / Tutorial Name](https://example.com) - Short description.`
- **Blogs & Newsletters**
  - *TODO:* `- [Blog / Newsletter Name](https://example.com) - Focus & audience.`

---

## Threat Modeling & Frameworks

> Frameworks, standards, and threat models for securing AI systems.

- **Standards & Guidelines**
  - *TODO:* `- [AI Risk Management / Security Standard](https://example.com) - What it covers.`
- **Threat Models & Taxonomies**
  - *TODO:* `- [Threat Model / Taxonomy Name](https://example.com) - Scope (e.g., data, training, inference, supply chain).`
- **Checklists & Best Practices**
  - *TODO:* `- [Checklist / Guide](https://example.com) - What stage of the AI lifecycle it targets.`

---

## Adversarial Machine Learning

> Classical and modern adversarial ML: attacks, defenses, and toolkits.

### Attacks

- Evasion attacks (adversarial examples).
- Poisoning & backdoor attacks.
- Model stealing / extraction.
- Membership and attribute inference.

*Example format:*

- *TODO:* `- **Paper / Tool Name** (Conf/Year) - Type of attack + key idea. [Paper](https://example.com) · [Code](https://example.com)`

### Defenses & Robust Training

- Robust optimization & certified defenses.
- Detection and monitoring of adversarial behavior.
- Defensive distillation and other mitigation techniques.

*Example format:*

- *TODO:* `- **Defense Name** (Conf/Year) - What threat it mitigates. [Paper](https://example.com) · [Code](https://example.com)`

### Toolkits & Libraries

- *TODO:* `- [Library / Toolkit Name](https://example.com) - Supported frameworks & main features.`

---

## LLM & GenAI Security

> Security of large language models, multimodal models, and agentic systems.

### Attacks

- Prompt injection & jailbreaks.
- Data exfiltration and policy bypass.
- Cross-tenant leakage, prompt leaking, training data extraction.
- Agentic / tool-using LLM attacks.

*Example format:*

- *TODO:* `- **Paper / Resource** (Year) - Threat type and key insight. [Paper](https://example.com)`

### Defenses & Guardrails

- Policy enforcement and content filters.
- Guardrail frameworks, safety layers, and proxies.
- Red teaming methodologies and evaluation frameworks.
- Attack / defense benchmarks for LLM security.

*Example format:*

- *TODO:* `- [Framework / Guardrail Tool](https://example.com) - How it integrates (proxy, SDK, gateway, etc.).`

### Tools & Platforms

- *TODO:* `- [Tool Name](https://example.com) - Hosted / self-hosted? What security problems it targets.`

---

## Privacy, Safety & Governance

> Privacy, safety, and governance for AI systems.

### Privacy Attacks & Defenses

- Membership inference / property inference.
- Differential privacy for model training.
- Federated learning security.

*Example format:*

- *TODO:* `- **Paper Name** (Conf/Year) - Attack/defense & setting (centralized / federated). [Paper](https://example.com)`

### Safety & Alignment

- Red teaming and safety evaluations.
- Safety policies for deployment.
- Human-in-the-loop mechanisms.

### Governance, Compliance & Policy

- AI risk management frameworks.
- Regulatory guidance and compliance checklists.
- Model cards, system cards, and documentation practices.

---

## Supply Chain & MLOps Security

> Securing the end-to-end AI supply chain: data, models, artifacts, and pipelines.

### Model & Dataset Supply Chain

- Model hub security and artifact verification.
- Dataset provenance and integrity.
- SBOM / AI-BOM / model cards for supply chain transparency.

### MLOps & CI/CD Security

- Secure training & deployment pipelines.
- Secrets management, identity and access management (IAM).
- Secure model registry & rollout strategies.

*Example format:*

- *TODO:* `- [Tool / Framework Name](https://example.com) - Where it fits in the MLOps lifecycle.`

---

## Infrastructure & Runtime Security

> Hardening the runtime environment and infrastructure around AI systems.

- Confidential computing and hardware-based isolation.
- Container / K8s security for model serving.
- Network security, API gateways, and rate limiting.
- Logging, monitoring, and audit trails for AI workloads.

*Example format:*

- *TODO:* `- [Solution / Project Name](https://example.com) - Which cloud / platform it supports.`

---

## Datasets & Benchmarks

> Datasets and benchmarks for AI security research and evaluation.

- Attack benchmarks.
- Defense and robustness benchmarks.
- LLM safety / security evaluation datasets.

*Example format:*

- *TODO:* `- [Dataset / Benchmark Name](https://example.com) - Tasks, threat types, and license.`

---

## Industrial & Domain-specific AI Security

> AI security resources focused on specific industries and verticals.

- **Industrial & OT / ICS**
  - *TODO:* `- [Resource / Case Study](https://example.com) - How AI is used and what security issues arise.`
- **Automotive & Mobility**
- **Healthcare & Bio**
- **Finance & Banking**
- **Other Vertical Domains**

---

## Related Awesome Lists & External Resources

> High-quality related lists. Avoid duplicating their content; link instead.

- *TODO:* `- [Awesome List Name](https://github.com/owner/repo) - Focus (e.g., LLM security, privacy, safety, etc.).`

---

## Contributing

Contributions are very welcome!

To keep this list **useful and focused**, please follow these rules:

1. **Relevance** – The resource must be clearly about *security of AI systems*.
2. **Quality over quantity** – We prefer a smaller list of strong, well-maintained resources.
3. **Public & stable links** – No paywalled or obviously temporary links when possible.
4. **One-line description** – Explain *why* the item is useful in a single concise sentence.
5. **Correct category** – Place the item under the most appropriate section.
6. **Alphabetical order within each section** (when it makes sense).

**How to contribute**

1. Fork this repo.
2. Create a branch for your changes.
3. Add your item(s) following the formatting rules.
4. Open a Pull Request with a short description (what you added and why).

You can also open issues for:

- Category suggestions
- Broken links
- Outdated or deprecated resources

---

## License

Choose a license that fits your preference, for example:

- [CC0-1.0](https://creativecommons.org/publicdomain/zero/1.0/) for a public domain-style list, or
- [MIT](https://opensource.org/licenses/MIT) if you prefer a permissive license.

> TODO: Replace this section with your actual license file and link.

