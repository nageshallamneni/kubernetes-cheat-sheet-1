### Service ###

Get replica controller.
~~~~
$ kubectl get rc

NAME        DESIRED   CURRENT   READY     AGE
webserver   6         6         6         1h
~~~~

Describe replica controller.
~~~~
$ kubectl describe rc

Name:         webserver
Namespace:    default 
Selector:     app=web
Labels:       app=web
Annotations:  kubectl.kubernetes.io/last-applied-configuration={"apiVersion":"v1","kind":"ReplicationController","metadata":{"annotations":{},"name":"webserver","namespace":"default"},"spec":{"replicas":3,"selector...
Replicas:     6 current / 6 desired
Pods Status:  6 Running / 0 Waiting / 0 Succeeded / 0 Failed
Pod Template:
  Labels:  app=web
  Containers:
   nginx:
    Image:        nginx:alpine
    Port:         80/TCP
    Host Port:    0/TCP
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Events:           <none>
~~~~

Scale replica controller
~~~~
$ kubectl scale --replicas=6 rc/webserver

replicationcontroller "webserver" scaled
~~~~

Delete replica controller
~~~~
$ kubectl delete rc webserver
~~~~