
# awesome-aisecurity

> 一个专注于 **AI 系统安全** 的资源清单 —— 覆盖威胁建模、对抗样本、LLM / 生成式 AI 安全、MLSecOps、隐私与治理等方向。

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

🌏 多语言版本：**简体中文** | [English](README.md)

---

## 初衷与范围说明

这个仓库关注的是 **“AI 本身的安全”**，而不是“用 AI 做安全”。

主要关注（大致）以下几个维度：

- 面向 AI / ML / LLM 的攻击与防御：对抗样本、数据投毒、模型窃取、隐私推断、越狱 / Jailbreak 等
- 模型与系统的鲁棒性、隐私与安全评估：工具、框架、基准、数据集
- 标准与治理：威胁建模、风险管理框架（如 NIST AI RMF 等）
- MLSecOps / MLOps / 供应链安全：数据、模型、流水线、依赖组件的全生命周期安全
- 行业场景：网络安全、工业 / OT、医疗、自动驾驶等（后续会逐步丰富）

目标读者包括：安全研究人员、算法工程师、红蓝队、架构师，以及需要系统性思考“AI 成为攻击面”问题的从业者。

---

## 快速上手（Quick Start）

如果你刚开始接触 AI 安全，可以按下面三步走：

1. **先看整体威胁版图**

   - [MITRE ATLAS](https://atlas.mitre.org/) – 面向 AI/ML 系统的攻击战术与技术知识库，类似 AI 版 ATT&CK。
   - [MITRE Adversarial ML Threat Matrix](https://github.com/mitre/advmlthreatmatrix) – 用 ATT&CK 风格梳理机器学习系统的攻击路径与案例。
   - [NIST AI Risk Management Framework (AI RMF 1.0)](https://www.nist.gov/itl/ai-risk-management-framework) – NIST 的 AI 风险管理框架，从治理、风险、度量等维度给出方法。
   - [OWASP Machine Learning Security Top 10](https://owasp.org/www-project-machine-learning-security-top-10/) – 总结机器学习系统的十大安全风险。
   - [OWASP Top 10 for Large Language Model Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/) – 面向 LLM 应用的十大安全风险（提示词注入、数据泄露等）。

2. **用工具“上手做一遍”**

   - [Adversarial Robustness Toolbox (ART)](https://github.com/Trusted-AI/adversarial-robustness-toolbox) – IBM / LF AI 社区维护的 ML 安全工具箱，支持逃逸、投毒、模型窃取与隐私推断等攻击与防御。
   - [CleverHans](https://github.com/cleverhans-lab/cleverhans) – 经典对抗样本库，可用于构造攻击与防御、做鲁棒性基准。
   - [Foolbox](https://github.com/bethgelab/foolbox) – 基于 PyTorch / TF / JAX 的对抗攻击工具箱，适合快速做鲁棒性实验。
   - [Giskard](https://github.com/Giskard-AI/giskard-oss) – 自动检测 ML / LLM 应用中的性能、偏差与安全问题。
   - [garak](https://github.com/NVIDIA/garak) – LLM 漏洞扫描工具，支持越狱、数据泄露、错误信息等多种检查。

3. **把安全能力融入工程与运维（MLSecOps）**

   - [awesome-MLSecOps](https://github.com/RiccardoBiosas/awesome-MLSecOps) – 围绕 MLSecOps 的工具与文章清单。
   - [awesome-llm-security](https://github.com/corca-ai/awesome-llm-security) – LLM 安全相关工具与文档。
   - [Awesome LM SSP](https://github.com/CryptoAILab/Awesome-LM-SSP) – 大模型安全 / 安全性 / 隐私相关的论文与资料合集。

想要参与贡献的话，可以直接跳到 [贡献指南](#贡献指南)。

---

## 目录

- [初衷与范围说明](#初衷与范围说明)
- [快速上手（Quick Start）](#快速上手quick-start)
- [1. 威胁建模与框架](#1-威胁建模与框架)
- [2. 对抗机器学习（Adversarial ML）](#2-对抗机器学习adversarial-ml)
- [3. LLM 与生成式 AI 安全](#3-llm-与生成式-ai-安全)
- [4. 隐私、安全性与治理](#4-隐私安全性与治理)
- [5. MLSecOps、MLOps 与供应链安全](#5-mlsecopsmlops-与供应链安全)
- [6. 数据集与基准（Benchmarks）](#6-数据集与基准benchmarks)
- [7. 学习资料与教程](#7-学习资料与教程)
- [8. 行业 / 领域场景的 AI 安全](#8-行业--领域场景的-ai-安全)
- [9. 相关 Awesome 清单](#9-相关-awesome-清单)
- [贡献指南](#贡献指南)
- [项目状态与规划](#项目状态与规划)
- [License](#license)

---

## 1. 威胁建模与框架

### 1.1 通用 AI / ML 威胁建模

- [MITRE ATLAS](https://atlas.mitre.org/) – 面向 AI/ML 系统攻击战术与技术的知识库，可用于威胁建模、攻防推演。
- [MITRE Adversarial ML Threat Matrix](https://github.com/mitre/advmlthreatmatrix) – 以 ATT&CK 风格整理 ML 系统的攻击路径、案例与防护思路。
- [OWASP Machine Learning Security Top 10](https://owasp.org/www-project-machine-learning-security-top-10/) – 总结机器学习系统各阶段的十大风险。
- [OWASP Top 10 for Large Language Model Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/) – 针对 LLM 应用的“十大安全风险”清单。
- [ML Security Cheat Sheet](https://mlsec.dev/) – 面向入门者的机器学习安全速查表，涵盖基本威胁与概念。

### 1.2 风险管理、治理与标准

- [NIST AI Risk Management Framework (AI RMF 1.0)](https://www.nist.gov/itl/ai-risk-management-framework) – NIST 发布的 AI 风险管理框架，从治理、风险、评估与管理等环节给出结构化方法。
- *SoK: Security and Privacy in Machine Learning* – 对 ML 安全与隐私威胁 / 防御进行系统化梳理的论文（Papernot 等）。
- *SoK: Data Reconstruction Attacks Against Machine Learning Models* – 聚焦数据重构攻击的威胁、度量与基准。
- *SoK: Data Minimization in Machine Learning* – 从数据最小化视角讨论 ML 生命周期中的隐私与安全。

---

## 2. 对抗机器学习（Adversarial ML）

### 2.1 工具与库

- [Adversarial Robustness Toolbox (ART)](https://github.com/Trusted-AI/adversarial-robustness-toolbox) – 覆盖逃逸、投毒、模型窃取、隐私推断等攻击与防御的 Python 工具箱。
- [CleverHans](https://github.com/cleverhans-lab/cleverhans) – 经典对抗样本库，为模型鲁棒性评估提供基准攻击与防御实现。
- [Foolbox](https://github.com/bethgelab/foolbox) – 支持 PyTorch / TensorFlow / JAX 的对抗攻击库，适合快速 benchmark。
- [AdvBox](https://github.com/advboxes/AdvBox) – 支持多框架、多场景的对抗样本工具箱（含黑盒攻击等）。
- [RobustBench](https://robustbench.github.io/) – 对抗鲁棒模型与标准化评测的集合，附带库与 leaderboard。

### 2.2 综述与代表性论文

- *Security Matters: A Survey on Adversarial Machine Learning* – 系统梳理对抗机器学习的攻击 / 防御思路。
- *SoK: Security and Privacy in Machine Learning* – 从安全与隐私视角系统总结 ML 威胁与防护。
- *Adversarial Machine Learning Attacks and Defense Methods in the Cyber Security Domain* – 聚焦网络安全场景下的对抗 ML 攻击与防御（Rosenberg 等）。
- *Adversarial Machine Learning: A Survey on the Influence of Different Attacks on Deep Learning Models* – 概述不同攻击对深度学习模型的影响。
- *Defense Strategies for Adversarial Machine Learning* – 综合讨论防御策略与局限性。

---

## 3. LLM 与生成式 AI 安全

### 3.1 指南与风险分类

- [OWASP Top 10 for Large Language Model Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/) – LLM 应用风险的“官方入门清单”。
- [OWASP LLM Top 10 非官方日文翻译](https://github.com/coky-t/owasp-top-10-for-large-language-model-applications-ja) – 日语读者可参考。
- [open-source-llm-scanners](https://github.com/psiinon/open-source-llm-scanners) – 开源 LLM 安全扫描工具列表。

### 3.2 工具与框架

- [garak](https://github.com/NVIDIA/garak) – LLM 漏洞扫描工具，可测试幻觉、越狱、数据泄露、毒性内容等。
- [LLM Guard](https://github.com/protectai/llm-guard) – 用于 LLM 交互安全加固的工具包（输入校验、输出过滤等）。
- [DeepTeam](https://github.com/confident-ai/deepteam) – 面向 LLM 系统红队 / 渗透测试的开源框架。
- [Giskard](https://github.com/Giskard-AI/giskard-oss) – 自动发现 ML / LLM 应用中的性能、偏差与安全问题。
- [cyber-security-llm-agents](https://github.com/NVISOsecurity/cyber-security-llm-agents) – 基于 AutoGen 的网络安全领域 LLM Agent 集合。

### 3.3 基准与数据集

- [JailbreakBench](https://github.com/JailbreakBench/jailbreakbench) – 面向 LLM 越狱攻击的公开鲁棒性基准与评测库。
- [JBB-Behaviors 数据集](https://huggingface.co/datasets/JailbreakBench/JBB-Behaviors) – 用于测试 LLM 产生有害内容的“滥用行为”数据集。
- *JailbreakBench: An Open Robustness Benchmark for Jailbreaking Large Language Models* – NeurIPS 2024 基准论文。
- （WIP）其它越狱 / 提示词注入相关数据集：AdvBench、HarmBench、JailbreakDiffBench、JailbreakV 等。

---

## 4. 隐私、安全性与治理

- [NIST AI RMF 1.0](https://www.nist.gov/itl/ai-risk-management-framework) – 从组织治理、风险识别、度量与管理等角度定义 AI 风险管理框架。
- *SoK: Security and Privacy in Machine Learning* – 涵盖模型反演、成员推断等隐私攻击及相应防御。
- *SoK: Security and Privacy Risks of Healthcare AI* – 聚焦医疗领域 AI 的安全与隐私风险。
- *SoK: Data Minimization in Machine Learning* – 从数据最小化角度讨论 ML 系统中数据使用与暴露。
- *SoK: Data Reconstruction Attacks Against Machine Learning Models* – 系统化梳理数据重构攻击类型与度量方法。

---

## 5. MLSecOps、MLOps 与供应链安全

- [awesome-MLSecOps](https://github.com/RiccardoBiosas/awesome-MLSecOps) – 聚焦 MLSecOps（ML + DevSecOps）的工具与资源清单。
- [MLSecOps-DevSecOps-Awesome](https://github.com/noobpk/MLSecOps-DevSecOps-Awesome) – 结合 MLSecOps 与 DevSecOps 的精选资源。
- [MLSecOps 仓库](https://github.com/Benjamin-KY/MLSecOps) – 关注将机器学习集成到安全运营中的实践与策略。
- [OWASP Machine Learning Security Top 10](https://owasp.org/www-project-machine-learning-security-top-10/) – 非常适合与 MLOps 流水线结合的风险视图。
- [Automating ML Security Checks using CI/CD](https://circleci.com/blog/automating-machine-learning-security-checks-using-ci-cd/) – 如何在 CI/CD 中加入 ML 安全检查的实践文章。
- [Analyzing the Security of Machine Learning Research Code](https://developer.nvidia.com/blog/analyzing-the-security-of-machine-learning-research-code/) – NVIDIA AI Red Team 关于 ML 研究代码安全性的经验总结。

---

## 6. 数据集与基准（Benchmarks）

### 6.1 常见扰动 / 污染鲁棒性

- [ImageNet-C](https://zenodo.org/records/2235448) – 在 ImageNet 验证集上施加多种常见扰动，用于评估模型在“非理想环境”下的鲁棒性。
- [CIFAR-10-C / CIFAR-100-C](https://zenodo.org/records/2535967) – 针对 CIFAR 系列的扰动鲁棒性基准（19 种扰动 × 5 个强度）。
- [RobustBench](https://robustbench.github.io/) – 整合了对抗鲁棒模型与标准化评测流程。

### 6.2 LLM 越狱与安全基准

- [JailbreakBench](https://github.com/JailbreakBench/jailbreakbench) – 面向 LLM 越狱攻击的公开基准与评测框架。
- [JBB-Behaviors 数据集](https://huggingface.co/datasets/JailbreakBench/JBB-Behaviors) – 包含 100 类滥用行为的安全测试数据集。
- 更多 Jailbreak / 安全性数据集：AdvBench、HarmBench、Qualifire prompt-injection benchmark、JailbreakDiffBench 等。

---

## 7. 学习资料与教程

### 7.1 课程、教程与速查表

- [ML Security Cheat Sheet](https://mlsec.dev/) – 为机器学习安全初学者准备的概念 / 威胁速查表。
- *Introduction to ML Security*（ELSA AI 课程模块） – 提供 Slides / 视频 / 代码示例的入门课程。
- *A Beginner's Guide to Adversarial Machine Learning* – 面向对抗 ML 入门者的大会教程演讲。
- *Five Essential Machine Learning Security Papers*（NCC Group Blog） – 精选 5 篇“必读” ML 安全论文并附解读。

### 7.2 书籍与长文

- *Machine Learning Security Principles* – 系统讲解 ML 安全原则与实践的书籍。
- *Machine Learning Security: The Ultimate Power Guide* – 关于 ML 威胁与防御的长篇入门指南。

---

## 8. 行业 / 领域场景的 AI 安全

> 该部分目前只放少量代表性资源，后续会重点补充工业 / OT / 关键基础设施等方向。

- *A Survey of Adversarial Machine Learning in Cyber Warfare* – 讨论对抗 ML 在网络战与军事场景中的应用与风险。
- *SoK: Security and Privacy Risks of Healthcare AI* – 分析医疗 AI 系统中的安全与隐私风险。
- 其它值得持续关注的方向：
  - 自动驾驶 / 交通领域的对抗样本与鲁棒性
  - 网络入侵检测（NIDS）中的对抗 ML
  - 工业控制（ICS / OT）环境中部署 AI 模型的威胁与防护

---

## 9. 相关 Awesome 清单

如果你需要更垂直或更重度的资源，可以参考：

- [awesome-adversarial-machine-learning（yenchenlin）](https://github.com/yenchenlin/awesome-adversarial-machine-learning) – 对抗 ML 论文、博客、演讲等的经典清单。
- [awesome-adversarial-machine-learning（man3kin3ko）](https://github.com/man3kin3ko/awesome-adversarial-machine-learning) – 更偏向“机器学习安全”大类的 Awesome 列表。
- [Awesome AI for Security](https://amanpriyanshu.github.io/Awesome-AI-For-Security/) – 聚焦“用 AI 做安全”（而不是“AI 的安全”）。
- [awesome-MLSecOps](https://github.com/RiccardoBiosas/awesome-MLSecOps) – MLSecOps 方向必读。
- [awesome-llm-security](https://github.com/corca-ai/awesome-llm-security) – LLM 安全相关工具与资源。
- [Awesome LM SSP](https://github.com/CryptoAILab/Awesome-LM-SSP) – 大模型安全 / 安全性 / 隐私阅读清单。
- [Awesome LLM4Security](https://github.com/liu673/Awesome-LLM4Security) – 中文语境下的 LLM 安全资料整理。
- [Awesome LLM Security Papers](https://github.com/kydahe/Awesome-LLM-Security-Papers) – 针对 LLM 系统安全的论文列表。
- [Awesome LLM Safety](https://github.com/ydyjya/Awesome-LLM-Safety) – LLM 安全性相关资源与教程。

---

## 贡献指南

欢迎各种形式的贡献，包括但不限于：补充链接、调整结构、增加新章节、翻译更多语言等。

### 可以贡献什么？

- 与 **AI 系统安全** 强相关的资源，例如：
  - 威胁建模、风险框架、合规与治理
  - 针对模型 / 数据 / 流水线的攻击与防御
  - 工具、开源库、数据集、基准、教程
- 可公开访问、相对稳定的链接（尽量避免 404 / 付费墙）。

### 格式约定

请尽量遵守以下约定：

1. 使用无序列表（`-`）添加条目。
2. 每行只放一个条目。
3. 推荐使用如下格式：

**工具 / 开源库**

```md
- [项目名](https://example.com) – 简要说明它做什么、为什么有用（尽量一句话说清楚）。
