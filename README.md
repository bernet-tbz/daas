# duk
Docker und Kubernetes

### Kubernetes Cluster (kind) erstellen

    kind create cluster --config kind-config.yaml --name kind --retain
    
**Dashboard und PersistentVolume**

    kubectl apply -f https://raw.githubusercontent.com/mc-b/lerncloud/master/data/DataVolume.yaml
    kubectl apply -f https://raw.githubusercontent.com/mc-b/lerncloud/master/addons/dashboard.yaml
    kubectl apply -f https://raw.githubusercontent.com/mc-b/lerncloud/master/addons/dashboard-admin.yaml 

**Metrics Server**

    kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml && \
    kubectl patch deployment metrics-server -n kube-system --type='json' -p='[{\"op\":\"add\",\"path\":\"/spec/template/spec/containers/0/args/-\",\"value\":\"--kubelet-insecure-tls\"}]'

**Ingress**

    kubectl label node kind-control-plane ingress-ready=true kubernetes.io/os=linux 
    kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.9.4/deploy/static/provider/kind/deploy.yaml
    
**Keep-Alive**
    
    docker ps --filter "name=kind" --format "{{.Names}}" | xargs -n1 docker update --restart unless-stopped    