# katy-at-home

stuff on my k3s machine running at home

## install k3s, helm3

1. install kubectl, alias k
2. install krew
3. k krew install ns
4. k krew install ctx
5. go
6. powerline go
7. k3s

* export INSTALL_K3S_EXEC=" --no-deploy servicelb --no-deploy traefik"
* export K3S_KUBECONFIG_MODE="664"
* curl -sfL <https://get.k3s.io> | sh -
* disable k3s servicelb (using metallb)
  * add `--disable servicelb` to /etc/systemd/system/k3s.service in section `ExecStart`
* add local storage (e.g. hard drives)  
  * add `--default-local-storage-path /data/usb1` because k3s manages the cm local-path-config -n kube-system. dont edit cm by hand unless you deploy local-path-provisioner by self

## basic install

1. metalllb

* helm repo add bitnami <https://charts.bitnami.com/bitnami>
* helm install metallb bitnami/metallb --namespace kube-system --set configInline.address-pools[0].name=default --set configInline.address-pools[0].protocol=layer2 --set configInline.address-pools[0].addresses[0]=192.168.0.240-192.168.0.250

1. ingress

* helm install nginx-ingress stable/nginx-ingress --namespace kube-system     --set defaultBackend.enabled=false

1. ?

* helm repo add stable <https://kubernetes-charts.storage.googleapis.com>

## apps

1. syncthing

* helm repo add k8s-at-home <https://k8s-at-home.com/charts/>
* helm template syncthing k8s-at-home/syncthing -f syncthing-values.yaml > my-syncthing.yaml
* k create ns syncthing
* k apply -f my-syncthing.yaml -n syncthing
