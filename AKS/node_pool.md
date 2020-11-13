

# 节点池
## 什么是节点池
在 Azure Kubernetes 服务 (AKS) 中，采用相同配置的节点分组成节点池。 节点池包含运行应用程序的底层 VM。 系统节点池和用户节点池是 AKS 群集的两种不同的节点池模式。 系统节点池主要用于托管关键System Pod（例如 CoreDNS 和 metrics-server）。 用户节点池主要用于托管Application Pod。 但是，如果希望在 AKS 群集中只有一个池，可以在系统节点池上计调度Application Pod。 每个 AKS 群集必须至少包含一个系统节点池，该池至少包含一个节点。

## 系统节点池和用户节点池
对于系统节点池，AKS 会自动为其节点分配`kubernetes.azure.com/mode:system`标签。 这使 AKS 倾向于在包含此标签的节点池上调度System Pod。 此标签不会阻止你在系统节点池上调度Application Pod。 但是，我们建议将关键System Pod 与Application Pod 隔离，以防配置错误或未授权的Application Pod 意外终止System Pod。 可以通过创建专用系统节点池来强制执行此行为。 使用 `CriticalAddonsOnly=true:NoSchedule` 污点可防止在系统节点池上调度Application Pod。

> Reference
> https://docs.microsoft.com/zh-cn/azure/aks/use-system-pools
> 