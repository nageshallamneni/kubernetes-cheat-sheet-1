### Pods ###

Get all pods
~~~~
$ kubectl get pods
~~~~

Get all pods with details
~~~~
$ kubectl get pods -o wide
~~~~

Get pods all namespace
~~~~
$ kubectl get pods --all-namespaces
~~~~

Get pods with specific namespace
~~~~
$ kubectl get pods --namespace=<namespace>
~~~~

Describe specific pod
~~~~
$ kubectl describe pod <podname>
~~~~

Run command to specific pod
~~~~
$ kubectl exec <podname> -it <command>
~~~~

Create pod with yaml file
~~~~
$ kubectl create -f pods/nginx.yaml
~~~~

Delete pod from yaml file
~~~~
$ kubectl delete -f pods/nginx.yaml
~~~~