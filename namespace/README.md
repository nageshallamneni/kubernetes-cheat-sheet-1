### Namespace ###

Get namespace
~~~~
$ kubectl get ns

NAME           STATUS    AGE
default        Active    5d
kube-public    Active    5d
kube-system    Active    5d
~~~~

Create namespace
~~~~
$ kubectl create ns applications

namespace "applications" created
~~~~

Set label to namespace
~~~~
$ kubectl label ns applications name=apps

namespace "applications" labeled
~~~~

Get namespace by label
~~~~
$ kubectl get ns -l name=apps

NAME           STATUS    AGE
applications   Active    2m
~~~~

Delete namespace
~~~~
$ kubectl delete ns applications

namespace "applications" deleted
~~~~