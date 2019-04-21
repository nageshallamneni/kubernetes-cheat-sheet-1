### Deployment ###

Get deploymenet
~~~~
$ kubectl get deploy --namespace=applications

NAME         DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
web-server   2         2         2            2           54s
~~~~

Scale deployment
~~~~
$ kubectl scale --replicas=4 deploy/web-server --namespace=applications

eployment.extensions "web-server" scaled
~~~~

Delete deployment
~~~~
$ kubectl delete deploy web-server --namespace=applications

deployment.extensions "web-server" deleted
~~~~