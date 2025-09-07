```bash
kubectl create ns gpu-operator
kubectl label --overwrite ns gpu-operator pod-security.kubernetes.io/enforce=privileged
```

```bash
kubectl get nodes -o json | jq '.items[].metadata.labels | keys | any(startswith("feature.node.kubernetes.io"))'
```

```bash
helm repo add nvidia https://helm.ngc.nvidia.com/nvidia \
 && helm repo update
```

```bash
helm install --wait --generate-name \
    -n gpu-operator --create-namespace \
    nvidia/gpu-operator \
    --version=v25.3.0 \
    --set mig.strategy=single
```

