# Pods

## Creating a pod

```console
~/k8s-workshops $ kubectl apply -f 3-pods/pod.yml
pod/simple-pod created
```

```console
~/k8s-workshops $ kubectl get pods
NAME         READY   STATUS    RESTARTS   AGE
simple-pod   1/1     Running   0          50s
```

## Lack of durability

```console
~/k8s-workshops $ kubectl delete pod simple-pod
pod "simple-pod" deleted
```

```console
~/k8s-workshops $ kubectl get pods
No resources found in default namespace.
```

## Investigating a pod

```console
~/k8s-workshops $ kubectl apply -f 3-pods/pod.yml
pod/simple-pod created
```

```console
~/k8s-workshops $ kubectl get pod simple-pod -o yaml
apiVersion: v1
kind: Pod
...
```

```console
~/k8s-workshops $ kubectl describe pod simple-pod
name: simple-pod
namespace: default
priority: 0
nodeName: k3d-k3s-default-server-0
...
```

```console
~/k8s-workshops $ kubectl logs simple-pod
```

## Executing commands inside pods/containers

```console
~/k8s-workshops $ kubectl exec -it simple-pod sh
~ $ ls
podinfo  ui
~ $ ps
PID   USER     TIME  COMMAND
    1 app       0:00 ./podinfo
   12 app       0:00 sh
   21 app       0:00 ps
~ $ exit
~/k8s-workshops $
```

```console
~/k8s-workshops $ kubectl delete pod simple-pod
pod "simple-pod" deleted
```

## Liveness probe

```console
~/k8s-workshops $ kubectl apply -f 3-pods/liveness-pod.yml
pod/liveness-pod created
```

```console
~/k8s-workshops $ kubectl exec -it liveness-pod -- curl -XPOST localhost:9898/readyz/disable
```

```console
~/k8s-workshops $ kubectl get pods -w
NAME           READY   STATUS    RESTARTS   AGE
liveness-pod   0/1     Pending   0          0s
liveness-pod   0/1     Pending   0          0s
liveness-pod   0/1     ContainerCreating   0          0s
liveness-pod   1/1     Running             0          3s
liveness-pod   1/1     Running             1          20s
```

```console
~/k8s-workshops $ kubectl describe pod liveness-pod
```

```console
~/k8s-workshops $ kubectl delete pod liveness-pod
pod "liveness-pod" deleted
```

## Assigning CPU and memory resources to pods

```console
~/k8s-workshops $ kubectl apply -f 3-pods/resources-pod.yml
pod/resources-pod created
```

```console
~/k8s-workshops $ kubectl describe node minikube
```

```console
~/k8s-workshops $ kubectl delete pod resources-pod
pod "resources-pod" deleted
```

```console
~/k8s-workshops $ kubectl apply -f 3-pods/greedy-pod.yml
pod/greedy-pod created
```

```console
~/k8s-workshops $ kubectl get pods
NAME         READY   STATUS    RESTARTS   AGE
greedy-pod   0/1     Pending   0          5s
```

```console
~/k8s-workshops $ kubectl describe pod greedy-pod
Name:         greedy-pod
...
Events:
  Type     Reason            Age        From               Message
  ----     ------            ----       ----               -------
  Warning  FailedScheduling  <unknown>  default-scheduler  0/1 nodes are available: 1 Insufficient cpu, 1 Insufficient memory.
```

```console
~/k8s-workshops $ kubectl delete pod greedy-pod
pod "greedy-pod" deleted
```

## Forwarding port to a pod

```console
~/k8s-workshops $ kubectl apply -f 3-pods/pod.yml
pod/simple-pod created
```

```console
~/k8s-workshops $ kubectl port-forward pod/simple-pod 9898:9898
Forwarding from 127.0.0.1:9898 -> 9898
Forwarding from [::1]:9898 -> 9898
Handling connection for 9898
```

`localhost:9898`

![podinfo frontend](podinfo.png)

```console
~/k8s-workshops $ kubectl delete pod simple-pod
pod "simple-pod" deleted
```
