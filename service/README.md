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
This is the default Service Type, only reachable from within the cluster. Consider this as an internal load balancer.

![ClusterIP](https://1.bp.blogspot.com/-dXszbTZ3eB4/XL6o8epTy9I/AAAAAAAADPg/BLo1uJtzY_MPcL6YhWg426MRU05sjQx8QCLcBGAs/s1600/clusterip.jpeg)

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
A NodePort is an open port (30000–32767) on every node of your cluster. Kubernetes transparently routes incoming traffic on the NodePort to your service, even if your application is running on a different node.

![NodePort](https://1.bp.blogspot.com/-iOoMWu1gJgw/XL6o8jtoK9I/AAAAAAAADPk/pL8zlEZ1dT0PolPUipPF-sbpF3FS2QW5QCLcBGAs/s1600/nodeport.jpeg)

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


#### Create service load balancer ####
Using a LoadBalancer service type automatically deploys an external load balance.

![LoadBalancer](https://4.bp.blogspot.com/-gMlVttdhnlE/XL6o8fLZAvI/AAAAAAAADPc/hhOYR4BYM-cuz7nfO1W0q3grHPYXO6RMwCLcBGAs/s1600/lb.jpeg)

~~~~
$ kubectl apply -f service/yaml/svc-loadbalancer.yaml
service/web-service-loadbalance created

$ kubectl describe svc web-service-loadbalance --namespace=webapps
Name:                     web-service-loadbalance
Namespace:                webapps
Labels:                   <none>
Annotations:              kubectl.kubernetes.io/last-applied-configuration:
                            {"apiVersion":"v1","kind":"Service","metadata":{"annotations":{},"name":"web-service-loadbalance","namespace":"webapps"},"spec":{"external...
Selector:                 app=nginx-web-apps
Type:                     LoadBalancer
IP:                       10.233.18.154
External IPs:             188.166.207.187
Port:                     <unset>  80/TCP
TargetPort:               80/TCP
NodePort:                 <unset>  30080/TCP
Endpoints:                10.233.102.4:80,10.233.85.2:80
Session Affinity:         None
External Traffic Policy:  Cluster
Events:                   <none>

Note:
Need forwarding rule from balancer 188.166.207.187:80 to <ipworker>:30080

URL: http://188.166.207.187
~~~~

#### Create service ingress ####

![Ingress](https://4.bp.blogspot.com/-2ToTggM7hm4/XL6o9WJ-2QI/AAAAAAAADPw/St12QMgoT8o3kwATpMLUAqQJl3Em0L-ggCEwYBhgL/s1600/nodeport.png)