# sre-agent-gitops: : GitOps 环境下的智能运维助手

一个基于 GitOps 理念构建的自动化运维系统，通过 ArgoCD 托管核心组件（Ollama 大模型、SRE-Agent 智能代理、Prometheus 监控），实现 Kubernetes 集群的**自动感知-智能决策-自主执行**全流程运维

## 项目简介

SRE-Agent 是系统的核心智能组件（使用 Go 语言开发），其工作流如下：
1. **环境感知**：定期查询 Prometheus 获取 Kubernetes 集群指标（如 Pod 状态、资源使用率、服务健康度等）；
2. **智能决策**：将监控数据输入 Qwen 0.5B 大模型，分析异常并生成具体运维决策（如重启故障 Pod、扩容负载、调整资源限制等）；
3. **自动执行**：通过 Kubernetes API Server 执行决策，实现无人干预的运维操作。

整个系统通过 GitOps 模式由 ArgoCD 托管，所有配置变更通过 Git 仓库管理，确保运维流程可追溯、可版本化。

## 组件构成
- **SRE-Agent**：Go 语言开发的智能代理，负责串联感知、决策、执行流程；
- **ArgoCD**：GitOps 核心工具，托管并同步 Ollama、SRE-Agent、Prometheus 的部署配置；
- **Ollama + Qwen 0.5B**：轻量级本地大模型，提供运维决策的 AI 推理能力；
- **Prometheus**：监控指标采集与存储，为 SRE-Agent 提供环境感知数据。
- **K8s**: sre-agent调用api-server执行决策

