# katy-at-home
stuff on my k3s machine running at home

# install k3s, helm3

1. kubectl alias k
2. install krew
3. k krew install ns
4. k krew install ctx
5. go
6. powerline go
7. k3s
* export INSTALL_K3S_EXEC=" --no-deploy servicelb --no-deploy traefik"
* export K3S_KUBECONFIG_MODE="644"
* curl -sfL https://get.k3s.io | sh -


# install charts

1. ingress
* helm install nginx-ingress stable/nginx-ingress --namespace kube-system     --set defaultBackend.enabled=false

2. metalllb
* helm repo add bitnami https://charts.bitnami.com/bitnami
* helm install metallb bitnami/metallb --namespace kube-system --set configInline.address-pools[0].name=default --set configInline.address-pools[0].protocol=layer2 --set configInline.address-pools[0].addresses[0]=192.168.0.240-192.168.0.250


3. ?
* helm repo add stable https://kubernetes-charts.storage.googleapis.c
om 
*  

## apps

1. syncthing
* helm repo add k8s-at-home https://k8s-at-home.com/charts/
* helm render syncthing k8s-at-home/syncthing > syncthing-rendered.yaml