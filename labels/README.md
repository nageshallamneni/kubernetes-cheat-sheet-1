### Labels ###

Show labels
~~~~
$ kubectl get pods --show-labels
~~~~

Set label to pods
~~~~
$ kubectl label pods <metadata.name> <key>:<value> 

Ex:
Set pod mongodb to label name=db
$ kubectl label pods mongodb name=db
~~~~

Filter label with specific value
~~~~
$ kubectl get pods --selector name=web

or

$ kubectl get pods -l name=web
~~~~

Filter label with multiple value
~~~~
$ kubectl get pods -l 'env in (web,db)'
~~~~



