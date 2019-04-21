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

deployment.extensions "web-server" scaled
~~~~

Rollback deployment
~~~~
Create
$ kubectl apply -f deployment/yaml/nginx-deploy.yaml
deployment.apps "web-server" created

Update
$ kubectl apply -f deployment/yaml/nginx-deploy-update.yaml
deployment.apps "web-server" configured

History
$ kubectl rollout history deploy web-server --namespace=applications
deployments "web-server"
REVISION  CHANGE-CAUSE
1         <none>
2         <none>

Rollback
$ kubectl rollout undo deploy web-server --namespace=applications --to-revision=1
deployment.apps "web-server" 
~~~~

Delete deployment
~~~~
$ kubectl delete deploy web-server --namespace=applications

deployment.extensions "web-server" deleted
~~~~