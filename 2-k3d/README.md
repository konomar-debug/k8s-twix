# k3d

```console
~/k8s-workshops $ k3d cluster create -p "8081:80@loadbalancer" -p "8082:443@loadbalancer" --image rancher/k3s:v1.29.6-k3s2 --k3s-arg "--resolv-conf=/etc/rancher/k3s/resolv.conf@server:0" -v "/etc/rancher/k3s/resolv.conf:/etc/rancher/k3s/resolv.conf" -v "/etc/rancher/k3s/registries.yaml:/etc/rancher/k3s/registries.yaml" -v "/etc/rancher/k3s/cert.d:/etc/rancher/k3s/cert.d" 
```
```console
~/k8s-workshops $ k3d kubeconfig get k3s-default
```




```console
~/k8s-workshops $ k3d help
https://k3d.io/
k3d is a wrapper CLI that helps you to easily create k3s clusters inside docker.
Nodes of a k3d cluster are docker containers running a k3s image.
All Nodes of a k3d cluster are part of the same docker network.
```

```console
~/k8s-workshops $ k3d cluster list
NAME          SERVERS   AGENTS   LOADBALANCER
k3s-default   1/1       0/0      true
```

```console
~/k8s-workshops $ kubectl get node -o wide
NAME                       STATUS   ROLES                  AGE     VERSION        INTERNAL-IP   EXTERNAL-IP   OS-IMAGE           KERNEL-VERSION       CONTAINER-RUNTIME
k3d-k3s-default-server-0   Ready    control-plane,master   9m38s   v1.28.8+k3s1   172.18.0.3    <none>        K3s v1.28.8+k3s1   5.15.0-119-generic   containerd://1.7.11-k3s2```

```console
~/k8s-workshops $ kubectl describe node k3d-k3s-default-server-0

```

## Multi-node K8s cluster
