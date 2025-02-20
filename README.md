# Certified Kubernetes Administrator (CKA) Exam Cheat Sheet

## Exam Curriculum (Q1 2025)

[CKA_Curriculum_v1.31.pdf](https://github.com/cncf/curriculum/blob/master/CKA_Curriculum%20Coming%20Soon%20Q1%202025.pdf):

# 10% - Storage

- Implement storage classes and dynamic volume provisioning
- Configure volume types, access modes and reclaim policies
- Manage persistent volumes and persistent volume claims

# 15% - Workloads and Scheduling

- Understand application deployments and how to perform rolling update and rollbacks
- Use ConfigMaps and Secrets to configure applications
- Configure workload autoscaling
- Understand the primitives used to create robust, self-healing, application deployments
- Configure Pod admission and scheduling (limits, node affinity, etc.)

# 20% - Servicing and Networking

- Understand connectivity between Pods
- Define and enforce Network Policies
- Use ClusterIP, NodePort, LoadBalancer service types and endpoints
- Use the Gateway API to manage Ingress traffic
- Know how to use Ingress controllers and Ingress resources
- Understand and use CoreDNS

# 30% - Troubleshooting

- Troubleshoot clusters and nodes
- Troubleshoot cluster components
- Monitor cluster and application resource usage
- Manage and evaluate container output streams
- Troubleshoot services and networking

# 25% - Cluster Architecture, Installation and Configuration

- Manage role based access control (RBAC)
- Prepare underlying infrastructure for installing a Kubernetes cluster
- Create and manage Kubernetes clusters using kubeadm
- Manage the lifecycle of Kubernetes clusters
- Implement and configure a highly-available control plane
- Use Helm and Kustomize to install cluster components
- Understand extension interfaces (CNI, CSI, CRI, etc.)
- Understand CRDs, install and configure operators

upgrade kubeadm k8s

```
export version=1.31
export partial_version=1.31.0
export complete_version="${version}.0-1.1"

echo "deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v${version}/deb/ /" | sudo tee /etc/apt/sources.list.d/kubernetes.list

apt-mark unhold kubeadm && \
apt-get update && apt-get install -y kubeadm="${complete_version}" && \
apt-mark hold kubeadm

kubeadm upgrade apply "${partial_version}"

kubeadm upgrade node "${partial_version}"

apt-mark unhold kubelet kubectl && \
apt-get update && apt-get install -y kubelet="${complete_version}" kubectl="${complete_version}" && \
apt-mark hold kubelet kubectl

apt-mark unhold kubelet && \
apt-get update && apt-get install -y kubelet="${complete_version}" && \
apt-mark hold kubelet

systemctl daemon-reload
systemctl restart kubelet

```
