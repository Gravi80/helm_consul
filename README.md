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
## Helm
Helm defines a packaging format called `charts`. Charts are the things (packages) that we create, distribute, and consume.

#### Installing Helm
https://helm.sh/docs/intro/install/
```
brew install helm
helm version --short
```
Enable auto-completion
```
# bash
## in .bashrc
source <(helm completion bash)

# zsh
## in .zshrc
if [ $commands[helm] ]; then
  source <(helm completion zsh)
fi
```

* `helm search` : Search for charts in Helm Hub and Helm Repositories
* `helm install` : Install charts into Kubernetes
* `helm list` : List all releases of a given Kubernetes Namespace
* `helm show` : Show information about a chart
* `helm upgrade` : Upgrade a release to a new version of the underlying chart
* `helm pull` : Download and extract a chart from Helm hub or a Helm repository
* `helm repo` : Add, update, index, list, or remove chart repositories
* `helm package` : Create an `tgz` archive for the chart in the current folder


#### chart repository
A chart repository is an HTTP server that houses packaged charts and an `index.yaml` file. A chart repository can be any HTTP server that can serve YAML and .tar files and can answer GET requests. Therefore, You can use a Google Cloud Storage bucket, an Amazon S3 bucket, GitHub pages, or you can create a web server for hosting your chart.

```
helm repo list
helm search hub jenkins
helm repo add stable https://kubernetes-charts.storage.googleapis.com/
helm repo list
```


## Consul

#### Installing Consul
```
helm repo add hashicorp https://helm.releases.hashicorp.com
helm search repo hashicorp/consul
helm install -f consul/helm-consul-values.yaml hashicorp hashicorp/consul
kubectl get pods
kubectl port-forward hashicorp-consul-server-0 8500:8500
```

