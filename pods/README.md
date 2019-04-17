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
$ kubectl get pods --namespace=NAME_NAMESPACE
~~~~

Exec command to specific pods
~~~~
$ kubectl exec POD_NAME -it sh
​~~~~

Describe specific pod
~~~~
$ kubectl describe pod POD_NAME
~~~~
