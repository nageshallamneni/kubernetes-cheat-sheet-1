### Service ###

Get services
~~~~
$ kubectl get svc

NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   10.233.0.1   <none>        443/TCP   5d
~~~~

Create replica controller first as backend / enpoint
~~~~
$ kubectl apply -f service/yaml/nginx-rc.yaml
~~~~

Create service ClusterIP
~~~~
$ kubectl apply -f service/yaml/nginx-svc-clusterip.yaml
service "web-service" created

$ kubectl describe svc web-service --namespace=webapps
Name:              web-service
Namespace:         webapps
Labels:            app=web
Annotations:       kubectl.kubernetes.io/last-applied-configuration={"apiVersion":"v1","kind":"Service","metadata":{"annotations":{},"labels":{"app":"web"},"name":"web-service","namespace":"webapps"},"spec":{"ports":[{"...
Selector:          app=web
Type:              ClusterIP
IP:                10.233.60.180
Port:              <unset>  8080/TCP
TargetPort:        80/TCP
Endpoints:         10.233.105.146:80,10.233.74.241:80
Session Affinity:  None
Events:            <none>

URL:
$ curl -XGET http://10.233.60.180:8080
~~~~