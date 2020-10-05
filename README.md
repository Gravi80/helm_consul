# Helm & Consul
Playground for exploring Helm and Consul

#### K8s cluster setup
```
if [ ! -d "$HOME/kind-config" ]; then
  mkdir $HOME/kind-config
fi
if [ ! -f "$HOME/kind-config/config" ]; then
  touch $HOME/kind-config/config
fi
export KUBECONFIG="$HOME/kind-config/config"
kubectl config view
kind create cluster --config cluster-config.yaml --name heml-consul
```

```
export KUBECONFIG="$HOME/kind-config/config"
kubectl config get-contexts
kubectl cluster-info --context kind-heml-consul
kubectl config use-context kind-heml-consul
```
