# ClusterAPI with Talos Linux on Hetzner

```bash
# Set up mgmt cluster
kind create cluster
clusterctl init --bootstrap talos --control-plane talos --infrastructure hetzner

# Set up Hetzner hcloud token
kubectl create secret generic hetzner --from-literal=hcloud="$(cat ../HETZNER_TOKEN)"

# Build snapshot
export HCLOUD_TOKEN=$(cat ../HETZNER_TOKEN)
cd talos-hetzner
packer init .
packer build .

# Apply CAPI manifests
kubectl apply -f cluster.yaml
```
