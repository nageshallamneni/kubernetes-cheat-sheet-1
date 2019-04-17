### Pods ###

Get all pods
~~~~
$ kubectl get pods
~~~~

Get all pods with details
~~~~
$ kubectl get pods -o wide
~~~~

Get pods with specific namespace
~~~~
$ kubectl get pods --namespace=<name-space>
~~~~

Exec command to specific pods
~~~~
$ kubectl exec <pod_name> -it sh
​~~~~

Describe specific pod
~~~~
$ kubectl describe pod <pod_name>
~~~~
