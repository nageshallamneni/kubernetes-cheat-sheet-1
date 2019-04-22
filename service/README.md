## Service ##

#### Get services ####
~~~~
$ kubectl get svc

NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   10.233.0.1   <none>        443/TCP   5d
~~~~

Create replica controller first as backend / enpoint
~~~~
$ kubectl apply -f service/yaml/nginx-rc.yaml
~~~~

#### Create service ClusterIP ####

![ClusterIP](https://cdn-images-1.medium.com/max/800/1*I4j4xaaxsuchdvO66V3lAg.png)

~~~~
$ kubectl apply -f service/yaml/svc-clusterip.yaml
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

#### Create service nodePort ####

![NodePort](https://cdn-images-1.medium.com/max/800/1*CdyUtG-8CfGu2oFC5s0KwA.png)

~~~~
$ kubectl expose rc webserver --port=8888 --target-port=80 --type='NodePort' --namespace=webapps --name=web-service-nodeport
service/web-service-nodeport exposed
~~~~
~~~~
$ kubectl apply -f service/yaml/svc-nodeport.yaml
service/web-service-nodeport created

$ kubectl describe svc web-service-nodeport --namespace=webapps
Name:                     web-service-nodeport
Namespace:                webapps
Labels:                   <none>
Annotations:              kubectl.kubernetes.io/last-applied-configuration:
                            {"apiVersion":"v1","kind":"Service","metadata":{"annotations":{},"name":"web-service-nodeport","namespace":"webapps"},"spec":{"ports":[{"n...
Selector:                 app=web
Type:                     NodePort
IP:                       10.233.20.47
Port:                     http  8888/TCP
TargetPort:               80/TCP
NodePort:                 http  30080/TCP
Endpoints:                10.233.102.5:80,10.233.85.1:80
Session Affinity:         None
External Traffic Policy:  Cluster
Events:                   <none>

URL: http://<ip-server-host>:30080
~~~~


#### Create service ingress ####