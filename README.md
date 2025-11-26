# awesome-aisecurity

> A curated list of awesome resources on **AI system security** — threat modeling, adversarial ML, LLM & GenAI security, MLSecOps, privacy, governance, and more.

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

🌏 Read this in other languages: [简体中文](README_zh.md)
 💡 Contributions welcome! See [CONTRIBUTING](CONTRIBUTING.md) for details.
---

## Motivation & Scope

This list focuses on **security of AI systems themselves**, not just “AI for security”.

It covers (roughly):

- Attacks against AI models and pipelines (evasion, poisoning, extraction, inference, jailbreak, etc.)
- Defenses, evaluations, and benchmarks for robustness, privacy, and safety
- Frameworks, standards, and governance (e.g., threat modeling, risk management)
- MLSecOps / MLOps / supply chain security for ML & LLM systems
- Domain-specific AI security (e.g., cyber, industrial, healthcare) — to be expanded over time

The goal is to provide a **practical starting point** for researchers, engineers, red teamers, and security architects who need to reason about *AI as an attack surface*.

---

## Quick Start

If you’re new to AI security, here’s a suggested reading path:

1. **Understand the threat landscape**
   - [MITRE ATLAS](https://atlas.mitre.org/) – Knowledge base of adversary tactics & techniques against AI/ML systems.
   - [MITRE Adversarial ML Threat Matrix](https://github.com/mitre/advmlthreatmatrix) – ATT&CK-style matrix mapping attacks on ML.
   - [NIST AI Risk Management Framework (AI RMF 1.0)](https://www.nist.gov/itl/ai-risk-management-framework) – High-level risk & governance framework for AI.
   - [OWASP Machine Learning Security Top 10](https://owasp.org/www-project-machine-learning-security-top-10/) – Top risks for ML systems.
   - [OWASP Top 10 for Large Language Model Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/) – Top risks for LLM apps (prompt injection, data leakage, etc.).

2. **Get your hands dirty with tools**
   - [Adversarial Robustness Toolbox (ART)](https://github.com/Trusted-AI/adversarial-robustness-toolbox) – Comprehensive ML security toolbox (evasion, poisoning, extraction, inference).
   - [CleverHans](https://github.com/cleverhans-lab/cleverhans) – Classic adversarial examples library.
   - [Foolbox](https://github.com/bethgelab/foolbox) – Fast adversarial attacks across PyTorch, TensorFlow, JAX.
   - [Giskard](https://github.com/Giskard-AI/giskard-oss) – Open-source evaluation of performance, bias & security issues for ML/LLM apps.
   - [garak](https://github.com/NVIDIA/garak) – LLM vulnerability scanner (hallucination, leakage, jailbreaks, etc.).

3. **Operationalize (MLSecOps & LLM security)**
   - [awesome-MLSecOps](https://github.com/RiccardoBiosas/awesome-MLSecOps) – MLSecOps tools & resources.
   - [awesome-llm-security](https://github.com/corca-ai/awesome-llm-security) – Tools, docs, and projects about LLM security.
   - [Awesome LM SSP](https://github.com/CryptoAILab/Awesome-LM-SSP) – Reading list on large-model safety, security, privacy.

If you want to **contribute**, scroll down to [Contributing](#contributing).

---

## Table of Contents

- [Motivation & Scope](#motivation--scope)
- [Quick Start](#quick-start)
- [1. Threat Modeling & Frameworks](#1-threat-modeling--frameworks)
- [2. Adversarial Machine Learning](#2-adversarial-machine-learning)
- [3. LLM & GenAI Security](#3-llm--genai-security)
- [4. Privacy, Safety & Governance](#4-privacy-safety--governance)
- [5. MLSecOps, MLOps & Supply Chain Security](#5-mlsecops-mlops--supply-chain-security)
- [6. Datasets & Benchmarks](#6-datasets--benchmarks)
- [7. Learning Resources](#7-learning-resources)
- [8. Domain-Specific AI Security](#8-domain-specific-ai-security)
- [9. Related Awesome Lists](#9-related-awesome-lists)
- [Contributing](#contributing)
- [Project Status & Roadmap](#project-status--roadmap)
- [License](#license)

---

## 1. Threat Modeling & Frameworks

### 1.1 General AI/ML Threat Modeling

- [MITRE ATLAS](https://atlas.mitre.org/) – Knowledge base of adversary tactics & techniques targeting AI systems, aligned with MITRE ATT&CK-style tactics/techniques.
- [MITRE Adversarial ML Threat Matrix](https://github.com/mitre/advmlthreatmatrix) – ATT&CK-style framework mapping attacks on ML pipelines, with case studies and mitigations.
- [OWASP Machine Learning Security Top 10](https://owasp.org/www-project-machine-learning-security-top-10/) – Top 10 security issues for ML systems across the lifecycle (data, models, pipelines).
- [OWASP Top 10 for Large Language Model Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/) – LLM-specific risks such as prompt injection, insecure plugins, data exfiltration.
- [ML Security Cheat Sheet](https://mlsec.dev/) – High-level cheat sheet of concepts, threats, and categories in ML security.

### 1.2 Risk Management, Governance & Standards

- [NIST AI Risk Management Framework (AI RMF 1.0)](https://www.nist.gov/itl/ai-risk-management-framework) – Voluntary framework to manage AI risks and improve trustworthiness (governance, mapping, measuring, managing).
- *SoK: Security and Privacy in Machine Learning* – Systematization-of-Knowledge on ML security & privacy threats and defenses (Papernot et al., 2018).
- *SoK: Data Reconstruction Attacks Against Machine Learning Models* – Taxonomy and benchmark for reconstruction attacks on ML models.
- *SoK: Data Minimization in Machine Learning* – Framework for minimizing data exposure in ML pipelines.

---

## 2. Adversarial Machine Learning

### 2.1 Toolkits & Libraries

- [Adversarial Robustness Toolbox (ART)](https://github.com/Trusted-AI/adversarial-robustness-toolbox) – Python library for ML security (evasion, poisoning, extraction, inference); hosted by LF AI & Data.
- [CleverHans](https://github.com/cleverhans-lab/cleverhans) – Adversarial examples library for constructing attacks, building defenses, and benchmarking robustness.
- [Foolbox](https://github.com/bethgelab/foolbox) – Python toolbox for adversarial attacks on deep neural networks (PyTorch, TensorFlow, JAX).
- [AdvBox](https://github.com/advboxes/AdvBox) – Toolbox for generating adversarial examples across multiple DL frameworks and attack scenarios.
- [RobustBench](https://robustbench.github.io/) – Benchmark and library for adversarially robust models and standardized evaluation.

### 2.2 Surveys & Key Papers

(Use these to get a big-picture view before diving into specific attacks.)

- *Security Matters: A Survey on Adversarial Machine Learning* (Li et al.) – Broad survey of adversarial ML attacks and defenses.
- *SoK: Security and Privacy in Machine Learning* – Threat models and defense taxonomy for ML security (Papernot et al.).
- *Adversarial Machine Learning Attacks and Defense Methods in the Cyber Security Domain* – Focused on cyber security use cases (Rosenberg et al., ACM CSUR 2021).
- *Adversarial Machine Learning: A Survey on the Influence of Different Attacks on Deep Learning Models* – Comprehensive review of adversarial attacks and impacts.
- *Defense Strategies for Adversarial Machine Learning* – Survey of defense mechanisms and their limitations.

---

## 3. LLM & GenAI Security

### 3.1 Guidance & Taxonomies

- [OWASP Top 10 for Large Language Model Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/) – Canonical list of common LLM risks (prompt injection, data leakage, insecure tools).
- [OWASP LLM Top 10 – Unofficial Japanese Translation](https://github.com/coky-t/owasp-top-10-for-large-language-model-applications-ja) – Helpful for Japanese readers.
- [open-source-llm-scanners](https://github.com/psiinon/open-source-llm-scanners) – Curated list of open-source LLM security scanners.

### 3.2 Tools & Frameworks

- [garak](https://github.com/NVIDIA/garak) – LLM vulnerability scanner probing for jailbreaks, leakage, misinformation, toxicity, etc.
- [LLM Guard](https://github.com/protectai/llm-guard) – Security toolkit for LLM interactions (input validation, output filtering).
- [DeepTeam](https://github.com/confident-ai/deepteam) – LLM red teaming framework for penetration testing and safeguarding LLM systems.
- [Giskard](https://github.com/Giskard-AI/giskard-oss) – Automatic detection of performance, bias and security issues in ML/LLM applications.
- [cyber-security-llm-agents](https://github.com/NVISOsecurity/cyber-security-llm-agents) – Collection of AutoGen-based LLM agents for cyber security tasks.

### 3.3 Benchmarks & Datasets

- [JailbreakBench](https://github.com/JailbreakBench/jailbreakbench) – Open robustness benchmark for jailbreaking LLMs; includes the JBB-Behaviors dataset and evaluation library.
- [JBB-Behaviors dataset](https://huggingface.co/datasets/JailbreakBench/JBB-Behaviors) – 100 misuse behaviors for probing harmful outputs in LLMs.
- *JailbreakBench: An Open Robustness Benchmark for Jailbreaking Large Language Models* – NeurIPS 2024 benchmark paper.
- (WIP) Other jailbreak and prompt-injection datasets (AdvBench, HarmBench, Qualifire, etc.).

---

## 4. Privacy, Safety & Governance

- [NIST AI RMF 1.0](https://www.nist.gov/itl/ai-risk-management-framework) – Governance, risk, and compliance perspective for managing AI risks.
- *SoK: Security and Privacy in Machine Learning* – Covers model inversion, membership inference, and other privacy threats.
- *SoK: Security and Privacy Risks of Healthcare AI* – Domain-specific analysis of security & privacy issues in healthcare AI.
- *SoK: Data Minimization in Machine Learning* – On reducing data exposure across ML workflows.
- *SoK: Data Reconstruction Attacks Against Machine Learning Models* – Taxonomy and metrics for reconstruction attacks.

---

## 5. MLSecOps, MLOps & Supply Chain Security

- [awesome-MLSecOps](https://github.com/RiccardoBiosas/awesome-MLSecOps) – Curated tools, articles and resources for MLSecOps (ML + DevSecOps).
- [MLSecOps-DevSecOps-Awesome](https://github.com/noobpk/MLSecOps-DevSecOps-Awesome) – Resources at the intersection of MLSecOps & DevSecOps.
- [MLSecOps](https://github.com/Benjamin-KY/MLSecOps) – Repository focusing on integrating ML with security operations.
- [OWASP Machine Learning Security Top 10](https://owasp.org/www-project-machine-learning-security-top-10/) – Risk-centric view aligned with ML lifecycle & MLOps pipelines.
- [Automating ML Security Checks using CI/CD](https://circleci.com/blog/automating-machine-learning-security-checks-using-ci-cd/) – Tutorial on integrating ML security checks into CI/CD.
- [Analyzing the Security of Machine Learning Research Code](https://developer.nvidia.com/blog/analyzing-the-security-of-machine-learning-research-code/) – NVIDIA AI Red Team guidance on code-level ML security.

---

## 6. Datasets & Benchmarks

### 6.1 Robustness to Corruptions & Perturbations

- [ImageNet-C](https://zenodo.org/records/2235448) – ImageNet-based corruption benchmark for robustness to common corruptions.
- [CIFAR-10-C / CIFAR-100-C](https://zenodo.org/records/2535967) – Corruption benchmarks for CIFAR datasets (19 corruption types, 5 severity levels).
- [RobustBench](https://robustbench.github.io/) – Aggregates adversarially robust models and evaluation pipelines.

### 6.2 LLM Jailbreak & Safety Benchmarks

- [JailbreakBench](https://github.com/JailbreakBench/jailbreakbench) – Benchmark and dataset for jailbreak attacks on LLMs.
- [JBB-Behaviors dataset](https://huggingface.co/datasets/JailbreakBench/JBB-Behaviors) – Misuse behavior dataset for LLM security evaluation.
- (See also: AdvBench, HarmBench, JailbreakDiffBench, JailbreakV, etc.)

---

## 7. Learning Resources

### 7.1 Courses, Tutorials & Cheat Sheets

- [ML Security Cheat Sheet](https://mlsec.dev/) – Beginner-friendly overview of concepts and threats in ML security.
- *Introduction to ML Security* (ELSA AI) – Online module introducing ML security with slides, code, and video.
- *A Beginner's Guide to Adversarial Machine Learning* – Conference tutorial talk for newcomers.
- *Five Essential Machine Learning Security Papers* (NCC Group blog) – Curated list of key ML security papers with commentary.

### 7.2 Books & Long-form Guides

- *Machine Learning Security Principles* (Packt) – Book covering ML security concepts and best practices.
- *Machine Learning Security: The Ultimate Power Guide* – Long-form guide on threats and defenses in ML systems.

---

## 8. Domain-Specific AI Security

*(This section is intentionally small for now and will grow as we add more industry- and vertical-specific content.)*

- *A Survey of Adversarial Machine Learning in Cyber Warfare* – Discussion of adversarial ML in military and cyber warfare settings.
- *SoK: Security and Privacy Risks of Healthcare AI* – Domain-specific SoK on medical/healthcare AI.
- Tutorials & surveys on:
  - ML for network intrusion detection and its adversarial weaknesses
  - Adversarial ML for autonomous driving / navigation systems

---

## 9. Related Awesome Lists

If you’re looking for more specialized or overlapping lists:

- [awesome-adversarial-machine-learning (yenchenlin)](https://github.com/yenchenlin/awesome-adversarial-machine-learning) – Classic list of adversarial ML papers, blogs, and talks.
- [awesome-adversarial-machine-learning (man3kin3ko)](https://github.com/man3kin3ko/awesome-adversarial-machine-learning) – Broader “ML security” oriented awesome list.
- [Awesome AI for Security](https://amanpriyanshu.github.io/Awesome-AI-For-Security/) – AI/LLMs applied *to* security operations (as opposed to security *of* AI).
- [awesome-MLSecOps](https://github.com/RiccardoBiosas/awesome-MLSecOps) – MLSecOps-focused list.
- [awesome-llm-security](https://github.com/corca-ai/awesome-llm-security) – LLM security tools and documents.
- [Awesome LM SSP](https://github.com/CryptoAILab/Awesome-LM-SSP) – Safety, security, and privacy for large models.
- [Awesome LLM4Security](https://github.com/liu673/Awesome-LLM4Security) – Chinese-language curated resources on LLM security.
- [Awesome LLM Security Papers](https://github.com/kydahe/Awesome-LLM-Security-Papers) – Paper list focusing on LLM system security.
- [Awesome LLM Safety](https://github.com/ydyjya/Awesome-LLM-Safety) – LLM safety-related resources and tutorials.

---

## Contributing

Contributions are very welcome! This project is intentionally **minimal but opinionated** to start with; please help it grow.

### What we accept

- Resources **directly related to the security of AI systems**:
  - Threat modeling, frameworks, standards
  - Attacks & defenses (adversarial ML, LLM jailbreaks, poisoning, extraction, inference, etc.)
  - Tools, libraries, datasets, benchmarks
  - Good long-form explainers, tutorials, and courses
- Publicly accessible and reasonably stable links (no dead or private links, please).

### Formatting rules

Please:

1. Add items as unordered list items (`-`).
2. Keep one item per line.
3. Use these formats:

**Tools / libraries**

```md
- [Project Name](https://example.com) – One-line description of what it does and why it’s useful.
