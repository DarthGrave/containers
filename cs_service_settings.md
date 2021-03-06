---

copyright:
  years: 2014, 2020
lastupdated: "2020-02-10"

keywords: kubernetes, iks, node.js, js, java, .net, go, flask, react, python, swift, rails, ruby, spring boot, angular

subcollection: containers

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:preview: .preview}

# Default service settings for Kubernetes components
{: #service-settings}

Review the default settings for Kubernetes components, such as the `kube-apiserver`, `kubelet` or `kube-proxy` that {{site.data.keyword.containerlong_notm}} sets when you create your cluster. 
{: shortdesc}

## `kube-apiserver`
{: #kube-apiserver}

Review the default settings for the `kube-apiserver` master component in {{site.data.keyword.containerlong_notm}}. 
{: shortdesc}

| Category  |  Default settings |
|----------|------|
| Default pod tolerations | <ul><li><code>default-not-ready-toleration-seconds=600s</code></li><li><code>default-unreachable-toleration-seconds=600s</code></li></ul> | 
| Privileged pods | `allow-privileged=true` | 
| Request headers | <ul><li><code>requestheader-client-ca-file=/mnt/etc/kubernetes-cert/ca.pem</code></li><li><code>requestheader-username-headers=X-Remote-User</code></li><li><code>requestheader-group-headers=X-Remote-Group</code></li><li><code>requestheader-extra-headers-prefix=X-Remote-Extra-</code></li></ul> | 
| Admission controllers | <ul><li><code>NamespaceLifecycle</code></li><li><code>LimitRanger</code></li><li><code>ServiceAccount</code></li><li><code>DefaultStorageClass</code></li><li><code>Initializers</code> (Kubernetes 1.13 or earlier)</li><li><code>MutatingAdmissionWebhook</code></li><li><code>ValidatingAdmissionWebhook</code></li><li><code>ResourceQuota</code></li><li><code>PodSecurityPolicy</code></li><li><code>DefaultTolerationSeconds</code></li><li><code>StorageObjectInUseProtection</code></li><li><code>PersistentVolumeClaimResize</code></li><li><code>Priority</code> (Kubernetes 1.11 or later)</li><li><code>NodeRestriction</code> (Kubernetes 1.14 or later)</li><li><code>TaintNodesByCondition</code> (Kubernetes 1.14 or later)</li></ul> |
| Kube audit log config | <ul><li><code>audit-log-maxsize=128</code></li><li><code>audit-log-maxage=2</code></li><li><code>audit-log-maxbackup=2</code></li></ul> | 
| Feature gates | See [Feature gates](#feature-gates) | 
{: summary="The rows are read from left to right. The category is in the first column, with the description in the second column."}
{: caption="kube-apiserver settings" caption-side="top"}

## `kube-controller-manager`
{: #kube-controller-manager}

Review the default settings for the `kube-controller-manager` master component in {{site.data.keyword.containerlong_notm}}. 
{: shortdesc}


| Category  | Default settings |
|----------|------|
| Feature gates | See [Feature gates](#feature-gates)|
| Pod garbage collection threshold | `terminated-pod-gc-threshold=12500` | 
| Horizontal pod autoscaling | `horizontal-pod-autoscaler-use-rest-clients=true` |
{: summary="The rows are read from left to right. The category is in the first column, with the description in the second column."}
{: caption="kube-controller-manager settings" caption-side="top"}


## `kubelet`
{: #kubelet}

Review the default settings for the `kubelet` worker node component in {{site.data.keyword.containerlong_notm}}. 
{: shortdesc}


| Category  | Default settings |
|----------|------|
| Feature gates | See [Feature gates](#feature-gates). In addition, <code>CRIContainerLogRotation=true</code> is set. | 
| Pod manifest path | `pod-manifest-path=/etc/kubernetes/manifests` | 
| File check frequency | `file-check-frequency=5s` |
| Container logs | <ul><li><code>container-log-max-size=100Mi</code></li><li><code>container-log-max-files=3</code></li></ul> |
| Container runtime endpoint | `container-runtime-endpoint=unix:///run/containerd/containerd.sock` | 
| Kubernetes and system reserves | <ul><li><code>kube-reserved='memory=1051Mi,cpu=36m,pid=2048'</code></li><li><code>system-reserved='memory=1576Mi,cpu=54m,pid=2048'</code></li></ul> |
| CPU CFS quota | `cpu-cfs-quota-period=20ms` |
| cgroups | <ul><li><code>kubelet-cgroups=/podruntime/kubelet</code></li><li><code>runtime-cgroups=/podruntime/runtime</code></li></ul> | 
| Pod eviction | <ul><li><code>eviction-soft='memory.available<100Mi,nodefs.available<10%,imagefs.available<10%,nodefs.inodesFree<10%,imagefs.inodesFree<10%'</code></li><li><code>eviction-soft-grace-period='memory.available=10m,nodefs.available=10m,imagefs.available=10m,nodefs.inodesFree=10m,imagefs.inodesFree=10m'</code></li><li><code>eviction-hard='memory.available<100Mi,nodefs.available<5%,imagefs.available<5%,nodefs.inodesFree<5%,imagefs.inodesFree<5%'</code></li></ul> | 
{: summary="The rows are read from left to right. The category is in the first column, with the description in the second column."}
{: caption="kubelet settings" caption-side="top"}

## `kube-proxy`
{: #kube-proxy}

Review the default settings for the `kube-proxy` worker node component in {{site.data.keyword.containerlong_notm}}. 
{: shortdesc}

| Category  | Default settings |
|----------|------|
| Iptable settings | <ul><li><code>iptables-sync-period 300s</code></li><li><code>iptables-min-sync-period 5s</code></li></ul> |
| Proxy mode | `proxy-mode=iptables` |
| Feature gates | See [Feature gates](#feature-gates) | 
{: summary="The rows are read from left to right. The category is in the first column, with the description in the second column."}
{: caption="kube-proxy settings" caption-side="top"}

## Feature gates
{: #feature-gates}

Review the feature gates that are applied to all Kubernetes master and worker node components by default. 
{: shortdesc}

| Kubernetes version | Default feature gates |
|------|--------------|
| 1.17 | <ul><li><code>RuntimeClass=false</code></li><li><code>CustomCPUCFSQuotaPeriod=true</code></li><li><code>AllowInsecureBackendProxy=false</code></li></ul> | 
| 1.16 | <ul><li><code>RuntimeClass=false</code></li><li><code>CustomCPUCFSQuotaPeriod=true</code></li></ul> | 
| 1.15 | <ul><li><code>RuntimeClass=false</code></li><li><code>CustomCPUCFSQuotaPeriod=true</code></li></ul> | 
| 1.14 | <ul><li><code>RuntimeClass=false</code></li><li><code>SupportNodePidsLimit=true</code></li><li><code>CustomCPUCFSQuotaPeriod=true</code></li></ul> | 
| 1.13 | <ul><li><code>ExperimentalCriticalPodAnnotation=true</code></li></ul> | 
{: summary="The rows are read from left to right. The Kubernetes version is in the first column, with the default feature gates in the second column."}
{: caption="Overview of feature gates" caption-side="top"}

