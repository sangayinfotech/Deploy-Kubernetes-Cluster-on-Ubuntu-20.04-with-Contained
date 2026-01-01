# Kubernetes HA Cluster Setup (containerd + kubeadm) — Multi Master

This guide installs **containerd**, **Kubernetes (kubelet/kubeadm/kubectl)** and builds a **multi-master** cluster using a **load balancer IP**.

---

## Prerequisites

- Ubuntu nodes (Masters + Workers)
- Unique hostname + proper DNS/hosts entries
- Swap disabled on all nodes
- Load balancer VIP/IP ready (example: `LOAD_BALANCER_IP`)

### Disable swap (Run on all nodes)
```bash
sudo swapoff -a
sudo sed -i '/ swap / s/^\(.*\)$/#\1/g' /etc/fstab

Step 1: Install containerd (Run on ALL nodes)
1) Load required kernel modules
sudo modprobe overlay
sudo modprobe br_netfilter

cat <<EOF | sudo tee /etc/modules-load.d/containerd.conf
overlay
br_netfilter
EOF
