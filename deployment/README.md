### Deployment ###

Get deploymenet
~~~~
$ kubectl get deploy --namespace=applications

NAME         DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
web-server   2         2         2            2           54s
~~~~

Delete deployment
~~~~
$ kubectl delete deploy web-server --namespace=applications

deployment.extensions "web-server" deleted
~~~~