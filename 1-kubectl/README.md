# kubectl

```console
~/k8s-workshops $ kubectl --help
kubectl controls the Kubernetes cluster manager.
...
```

```console
~/k8s-workshops $ kubectl api-resources
NAME                              SHORTNAMES   APIGROUP                       NAMESPACED   KIND
bindings                                                                      true         Binding
...
```

```console
~/k8s-workshops $ kubectl get all -A
NAMESPACE     NAME                                   READY   STATUS    RESTARTS   AGE
kube-system   pod/coredns-5644d7b6d9-nvl4r           1/1     Running   0          3m14s
...
```

```console
~/k8s-workshops $ kubectl get pods -A -o wide
NAMESPACE     NAME                                     READY   STATUS      RESTARTS   AGE   IP           NODE                       NOMINATED NODE   READINESS GATES
kube-system   coredns-6799fbcd5-kdx5s                  1/1     Running     0          10h   10.42.0.6    k3d-k3s-default-server-0   <none>           <none>

```

```console
~/k8s-workshops $ kubectl get svc kubernetes -o yaml
apiVersion: v1
kind: Service
...
```
