## training plan 

<img src="plan.png">

### checking namespace and delete all the data 

```
kubectl config get-contexts 
CURRENT   NAME                          CLUSTER      AUTHINFO           NAMESPACE
*         kubernetes-admin@kubernetes   kubernetes   kubernetes-admin   ashu-space
 fire@ashutoshhs-MacBook-Air  ~/Desktop/deployapps  
 fire@ashutoshhs-MacBook-Air  ~/Desktop/deployapps  
 fire@ashutoshhs-MacBook-Air  ~/Desktop/deployapps  kubectl  get  all 
NAME                           READY   STATUS    RESTARTS       AGE
pod/ashuapp-7847f955c9-dn59t   1/1     Running   0              108m
pod/ashuapp-7847f955c9-kb79l   1/1     Running   0              107m
pod/ashuapp-7847f955c9-zclqx   1/1     Running   1 (3h9m ago)   18h
pod/ashupod-2                  1/1     Running   4 (109m ago)   17h

NAME                TYPE       CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
service/ashusvc2    NodePort   10.96.20.219     <none>        3000:30692/TCP   18h
service/yogeshvc1   NodePort   10.105.219.249   <none>        1234:31030/TCP   18h

NAME                      READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/ashuapp   3/3     3            3           18h

NAME                                 DESIRED   CURRENT   READY   AGE
replicaset.apps/ashuapp-7847f955c9   3         3         3       18h

NAME                                          REFERENCE            TARGETS   MINPODS   MAXPODS   REPLICAS   AGE
horizontalpodautoscaler.autoscaling/ashuapp   Deployment/ashuapp   0%/80%    3         20        3          18h
 fire@ashutoshhs-MacBook-Air  ~/Desktop/deployapps  kubectl delete all --all
pod "ashuapp-7847f955c9-dn59t" deleted
pod "ashuapp-7847f955c9-kb79l" deleted
pod "ashuapp-7847f955c9-zclqx" deleted
pod "ashupod-2" deleted
service "ashusvc2" deleted
service "yogeshvc1" deleted
deployment.apps "ashuapp" deleted
horizontalpodautoscaler.autoscaling "ashuapp" deleted

```
### Deploy private registry image in k8s 

### creating deployment yaml 

```
kubectl create deployment privateweb --image=phx.ocir.io/axmbtg8judkl/webapp:v1  --dry-run=client -o yaml  >privateapp.yaml

```
### private docker image can't be deployed bcz it need to pass auth details 

### Intro to secret 

<img src="secret.png">

### creating secret in personal namespace 

```
kubectl create secret 
Create a secret using specified subcommand.

Available Commands:
  docker-registry Create a secret for use with a Docker registry
  generic         Create a secret from a local file, directory, or literal value
  tls             Create a TLS secret

===

kubectl create secret docker-registry ashusec1  --docker-server=phx.ocir.io  --docker-username="axmbtdkl/lear@gmail.com"    --docker-password=")#Bi4PKZcfc"

```

### calling secret in pod of template of deployment 

<img src="secret1.png">

### deploy service from deployment using expose 

```
kubectl  get deploy
NAME         READY   UP-TO-DATE   AVAILABLE   AGE
privateweb   1/1     1            1           18m
 fire@ashutoshhs-MacBook-Air  ~/Desktop/deployapps  kubectl  expose deploy privateweb  --type LoadBalancer  --port 80 --name ashusvc1 
service/ashusvc1 exposed
 fire@ashutoshhs-MacBook-Air  ~/Desktop/deployapps  kubectl get  svc     
NAME       TYPE           CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
ashusvc1   LoadBalancer   10.103.122.83   <pending>     80:31351/TCP   13s

```

### NodePort vs LoadBalancer 

<img src="lb.png">

