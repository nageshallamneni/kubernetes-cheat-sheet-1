### Labels ###

Show labels
~~~~
$ kubectl get pods --namespace=<namespace_name> --show-labels
~~~~

Ex:
~~~~
$ kubectl get pods --namespace=applications --show-labels

NAME      READY   STATUS    RESTARTS   AGE     LABELS
apache    1/1     Running   0          3m36s   name=web
mongodb   1/1     Running   0          75s     <none>
nginx     1/1     Running   0          3m29s   name=web
~~~~


Set label to pods
~~~~
$ kubectl label pods <metadata.name> <key>:<value> 
~~~~

Ex:
~~~~
$ kubectl label pods mongodb name=db --namespace=applications

NAME      READY   STATUS    RESTARTS   AGE     LABELS
apache    1/1     Running   0          10m     name=web
mongodb   1/1     Running   0          7m44s   name=db
nginx     1/1     Running   0          9m58s   name=web
~~~~

Filter label with specific value
~~~~
$ kubectl get pods --selector name=web

or

$ kubectl get pods -l name=web
~~~~

Ex:
~~~~
$ kubectl get pod -l name=db --namespace=applications

NAME      READY   STATUS    RESTARTS   AGE
mongodb   1/1     Running   0          8m50s
~~~~

Filter label with multiple value
~~~~
$ kubectl get pods -l 'name in (web,db)'

NAME      READY   STATUS    RESTARTS   AGE
apache    1/1     Running   0          12m
mongodb   1/1     Running   0          10m
nginx     1/1     Running   0          12m
~~~~



