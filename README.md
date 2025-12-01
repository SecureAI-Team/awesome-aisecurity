# Awesome AI Security [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
<!--lint disable awesome-github-->

> Curated resources for securing AI/ML systems across threat modeling, adversarial ML, LLM security, governance, MLSecOps, and benchmarks.

 Read this in other languages: [¼òÌåÖÐÎÄ](README_zh.md)

 Contributions welcome! See [CONTRIBUTING](CONTRIBUTING.md) for details.

---

## Contents

- [ ASB Open Source Ecosystem](#-asb-open-source-ecosystem)
- [Quick Start](#quick-start)
- [1. Threat Modeling & Frameworks](#1-threat-modeling--frameworks)
- [2. Adversarial Machine Learning](#2-adversarial-machine-learning)
- [3. LLM & GenAI Security](#3-llm--genai-security)
- [4. Privacy, Safety & Governance](#4-privacy-safety--governance)
- [5. MLSecOps, MLOps & Supply Chain Security](#5-mlsecops-mlops--supply-chain-security)
- [6. Datasets & Benchmarks](#6-datasets--benchmarks)
- [7. Learning Resources](#7-learning-resources)
- [9. Related Awesome Lists](#9-related-awesome-lists)
- [Contributing](#contributing)
- [Project Status & Roadmap](#project-status--roadmap)
- [License](#license)

---

## ?? ASB Open Source Ecosystem

- [ASB Security Schema](https://github.com/SecureAI-Team/asb-security-schema) - Unified JSON schema for capturing AI security telemetry and sharing alerts across systems.
- [asb-secure-gateway](https://github.com/SecureAI-Team/asb-secure-gateway) - Reference gateway enforcing ASB schema with OPA policies for AI-native traffic.

---

## Quick Start

1. **Map the threat landscape**: skim [Section 1](#1-threat-modeling--frameworks) before picking tools or controls.
2. **Experiment with adversarial tooling**: start with the libraries in [Section 2](#2-adversarial-machine-learning) to understand attacker capability.
3. **Secure LLM applications**: apply the guidance and scanners in [Section 3](#3-llm--genai-security) as you build guardrails.
4. **Embed governance early**: use the risk and privacy references in [Section 4](#4-privacy-safety--governance) to keep regulators happy.
5. **Operationalize safeguards**: treat [Section 5](#5-mlsecops-mlops--supply-chain-security) as your MLSecOps checklist.

---

## 1. Threat Modeling & Frameworks

### 1.1 General AI/ML Threat Modeling

- [MITRE ATLAS](https://atlas.mitre.org/) - Tactics, techniques, and case studies for attacks on AI/ML systems.
- [MITRE Adversarial ML Threat Matrix](https://github.com/mitre/advmlthreatmatrix) - ATT&CK-style matrix translating ML pipeline attacks into concrete techniques.
- [ENISA Artificial Intelligence Threat Landscape](https://www.enisa.europa.eu/publications/artificial-intelligence-threat-landscape) - Comprehensive overview of AI attack surfaces, assets, and mitigations.
- [CISA/NSA Guidelines for Secure AI System Development](https://media.defense.gov/2024/Apr/29/2003456719/-1/-1/0/CSI_GUIDELINES_FOR_SECURE_AI_SYSTEM_DEVELOPMENT.PDF) - Joint principles for designing, deploying, and monitoring AI securely.
- [NCSC Patterns for Secure AI System Development](https://www.ncsc.gov.uk/collection/patterns-for-secure-ai-system-development) - Reusable architectural patterns for securing data, models, and tooling.

### 1.2 Risk Management, Governance & Standards

- [NIST AI Risk Management Framework (AI RMF 1.0)](https://www.nist.gov/itl/ai-risk-management-framework) - Voluntary framework covering governance, mapping, measuring, and managing AI risk.
- [NIST AI RMF Playbook](https://airmf.cio.gov/playbook/) - Practical implementation guidance, artifacts, and crosswalks for AI RMF adoption.
- [NIST AI RMF Profile: Generative AI](https://www.nist.gov/itl/ai-risk-management-framework/ai-risk-management-framework-profile-generative-ai) - Draft profile translating AI RMF tasks to GenAI-specific safeguards.

---

## 2. Adversarial Machine Learning

### 2.1 Toolkits & Libraries

- [Adversarial Robustness Toolbox (ART)](https://github.com/Trusted-AI/adversarial-robustness-toolbox) - Python library for evasion, poisoning, extraction, and inference attacks plus defenses.
- [CleverHans](https://github.com/cleverhans-lab/cleverhans) - Classic adversarial example framework for benchmarking robustness.
- [Foolbox](https://github.com/bethgelab/foolbox) - Unified interface for fast gradient-based and decision-based attacks across DL frameworks.
- [AdvBox](https://github.com/advboxes/AdvBox) - Attack generation across CV, NLP, and speech models with multi-framework support.
- [TextAttack](https://github.com/QData/TextAttack) - NLP-focused adversarial attack, augmentation, and training library.
- [AutoAttack](https://github.com/fra31/auto-attack) - Parameter-free ensemble of strong white-box attacks for reliable robustness evaluation.

### 2.2 Research & Surveys

- [Adversarial Attacks and Defences: A Survey](https://arxiv.org/abs/1810.00069) - Deep dive on threat models, attack classes, and countermeasures for DL systems.
- [Security Matters: A Survey on Adversarial Machine Learning](https://arxiv.org/abs/1810.07339) - Taxonomy linking attacker goals with defender controls across the ML lifecycle.
- [SoK: Security and Privacy in Machine Learning](https://oaklandsok.github.io/papers/papernot2018.pdf) - Foundational SoK covering threat models, privacy risks, and defense trade-offs.

---

## 3. LLM & GenAI Security

### 3.1 Guidance & Taxonomies

- [OWASP Top 10 for Large Language Model Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/) - Canonical list of LLM-specific risks and mitigations.
- [OWASP LLM Top 10  Unofficial Japanese Translation](https://github.com/coky-t/owasp-top-10-for-large-language-model-applications-ja) - Community translation of the OWASP LLM Top 10 for Japanese teams.
- [open-source-llm-scanners](https://github.com/psiinon/open-source-llm-scanners) - Catalog of scanners and fuzzers targeting LLM misuse cases.

### 3.2 Tools & Frameworks

- [garak](https://github.com/NVIDIA/garak) - LLM vulnerability scanner probing for jailbreaks, leakage, and safety failures.
- [LLM Guard](https://github.com/protectai/llm-guard) - Input/output filtering toolkit with regex, classifiers, and secret detectors for LLM apps.
- [DeepTeam](https://github.com/confident-ai/deepteam) - Red teaming orchestration framework for multi-agent LLM penetration testing.
- [Giskard](https://github.com/Giskard-AI/giskard-oss) - Evaluation suite catching bias, robustness, and security issues in ML/LLM pipelines.
- [cyber-security-llm-agents](https://github.com/NVISOsecurity/cyber-security-llm-agents) - AutoGen-based agents for offensive and defensive AI security tasks.

> Need LLM jailbreak benchmarks? Jump to [Section 6.2](#62-llm-jailbreak--safety-benchmarks).

---

## 4. Privacy, Safety & Governance

- [SoK: Data Reconstruction Attacks Against Machine Learning Models](https://www.usenix.org/conference/usenixsecurity25/presentation/wen) - Taxonomy and benchmarks for reconstruction attacks plus measurement guidance.
- [SoK: Security and Privacy Risks of Healthcare AI](https://arxiv.org/abs/2409.07415) - Sector-specific review of threats to clinical AI deployments.
- [SoK: Data Minimization in Machine Learning](https://arxiv.org/abs/2508.10836) - Framework for applying data-minimization principles throughout ML pipelines.

---

## 5. MLSecOps, MLOps & Supply Chain Security

- [MLSecOps](https://github.com/Benjamin-KY/MLSecOps) - Opinionated repo of processes, tooling, and templates for secure ML operations.
- [Automating ML Security Checks using CI/CD](https://circleci.com/blog/automating-machine-learning-security-checks-using-ci-cd/) - Guide for wiring poisoning, bias, and drift tests into pipelines.
- [Analyzing the Security of Machine Learning Research Code](https://developer.nvidia.com/blog/analyzing-the-security-of-machine-learning-research-code/) - NVIDIA AI Red Team playbook for auditing ML repos and dependencies.
- [ModelScan](https://github.com/protectai/modelscan) - Static and dynamic scanner for catching malicious or vulnerable model artifacts before deployment.

---

## 6. Datasets & Benchmarks

### 6.1 Robustness to Corruptions & Perturbations

- [ImageNet-C](https://zenodo.org/records/2235448) - Standard corruption benchmark to evaluate ML robustness to common noise patterns.
- [CIFAR-10-C / CIFAR-100-C](https://zenodo.org/records/2535967) - Corruption suites for CIFAR datasets spanning 19 perturbations at five severities.
- [RobustBench](https://robustbench.github.io/) - Leaderboard and library for adversarially robust models plus evaluation scripts.

### 6.2 LLM Jailbreak & Safety Benchmarks

- [JailbreakBench](https://github.com/JailbreakBench/jailbreakbench) - Open benchmark and evaluation harness for jailbreak robustness.
- [JBB-Behaviors dataset](https://huggingface.co/datasets/JailbreakBench/JBB-Behaviors) - 100 misuse behaviors for red teaming LLM outputs.
- [Heuristic Red Teaming](https://github.com/centerforaisafety/heuristic-red-teaming) - Prompt dataset and harness for stress-testing safety policies.

---

## 7. Learning Resources

- [ML Security Cheat Sheet](https://mlsec.dev/) - High-level primer on attack surfaces, threat models, and mitigation patterns.
- [Five Essential Machine Learning Security Papers](http://research.nccgroup.com/2023/07/05/five-essential-machine-learning-security-papers/) - NCC Group commentary on must-read academic work.
- [Machine Learning Security Principles (Packt)](https://www.packtpub.com/product/machine-learning-security-principles/9781801816975) - Book covering foundational concepts and defensive controls.
- [Responsible AI: Adversarial Attacks on LLMs (YouTube)](https://www.youtube.com/watch?v=7P5zYUX5R9s) - Conference talk demonstrating jailbreak techniques and mitigations.

---

## 9. Related Awesome Lists

- [awesome-adversarial-machine-learning (yenchenlin)](https://github.com/yenchenlin/awesome-adversarial-machine-learning)
- [awesome-adversarial-machine-learning (man3kin3ko)](https://github.com/man3kin3ko/awesome-adversarial-machine-learning)
- [Awesome AI for Security](https://amanpriyanshu.github.io/Awesome-AI-For-Security/)
- [awesome-MLSecOps](https://github.com/RiccardoBiosas/awesome-MLSecOps)
- [awesome-llm-security](https://github.com/corca-ai/awesome-llm-security)
- [Awesome LM SSP](https://github.com/CryptoAILab/Awesome-LM-SSP)
- [Awesome LLM4Security](https://github.com/liu673/Awesome-LLM4Security)
- [Awesome LLM Safety](https://github.com/ydyjya/Awesome-LLM-Safety)

---

## Contributing

We welcome high-signal resources that directly improve the security of AI systems.

### What we accept

- Threat modeling frameworks, governance standards, and incident handling references.
- Offensive and defensive research (adversarial ML, jailbreaks, poisoning, extraction, inference, safety testing).
- Production-ready tooling, datasets, benchmarks, and red teaming harnesses.
- Tutorials, talks, and books that teach practitioners how to secure AI systems.

### Formatting rules

1. Use unordered list items (`-`) and keep one resource per line.
2. Follow the format below and keep descriptions concise and plain English.

**Tools / libraries**

```md
- [Project Name](https://example.com) - One-line description of what it does and why its useful.
```

**Papers / posts / datasets**

```md
- *Paper or Post Title* - Short summary plus venue or publisher if relevant.
```

Add new entries near related content sections to keep the list curated and deduplicated. Please also double-check that added links are live and publicly accessible.

---

## Project Status & Roadmap

This list is early-stage and intentionally scoped to core security primitives. Near-term goals:

- Expand domains beyond generic ML/LLM (healthcare, industrial, safety-critical control).
- Track emerging GenAI-specific benchmarks and red teaming playbooks.
- Highlight production case studies once vetted.

Issues and PRs are welcome for suggestions.

---

## License

This project is released under [CC0 1.0](LICENSE). You can copy, modify, and reuse the list without asking permission.
