## training plan 

<img src="plan.png">

### revision 

<img src="rev.png">
### setup k8s cluster in local pc / laptop 

[INstall_link](https://minikube.sigs.k8s.io/docs/start/)

###  minikube 

<img src="min.png">

### checking 

```
minikube version 
minikube version: v1.24.0
commit: 76b94fb3c4e8ac5062daf70d60cf03ddcc0a741b

```

### kubectl for multiple cluster 

<img src="kube.png">

### start minikube cluster 

```
minikube  start  
😄  minikube v1.24.0 on Darwin 11.6
✨  Automatically selected the docker driver. Other choices: hyperkit, ssh
👍  Starting control plane node minikube in cluster minikube
🚜  Pulling base image ...
🔥  Creating docker container (CPUs=2, Memory=1986MB) ...
🐳  Preparing Kubernetes v1.22.3 on Docker 20.10.8 ...
    ▪ Generating certificates and keys ...
    ▪ Booting up control plane ...
    ▪ Configuring RBAC rules ...
🔎  Verifying Kubernetes components...
    ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5
🌟  Enabled addons: storage-provisioner, default-storageclass
🏄  Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default

```

### auto connected by kubectl 

```
kubectl  get  nodes
NAME       STATUS   ROLES                  AGE   VERSION
minikube   Ready    control-plane,master   71s   v1.22.3
```
### more minikube commands 

```
minikube status 
minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured

 fire@ashutoshhs-MacBook-Air  ~  minikube stop   
✋  Stopping node "minikube"  ...
🛑  Powering off "minikube" via SSH ...
🛑  1 node stopped.
 fire@ashutoshhs-MacBook-Air  ~  minikube status 
minikube
type: Control Plane
host: Stopped
kubelet: Stopped
apiserver: Stopped
kubeconfig: Stopped


```


### switching between / among the cluster 

```
 kubectl  config  get-contexts 
CURRENT   NAME                          CLUSTER      AUTHINFO           NAMESPACE
          kubernetes-admin@kubernetes   kubernetes   kubernetes-admin   
*         minikube                      minikube     minikube           default
 fire@ashutoshhs-MacBook-Air  ~/Desktop/deployapps  
 fire@ashutoshhs-MacBook-Air  ~/Desktop/deployapps  
 fire@ashutoshhs-MacBook-Air  ~/Desktop/deployapps  kubectl  config  use-context  kubernetes-admin@kubernetes
Switched to context "kubernetes-admin@kubernetes".
 fire@ashutoshhs-MacBook-Air  ~/Desktop/deployapps  
 fire@ashutoshhs-MacBook-Air  ~/Desktop/deployapps  kubectl  config  get-contexts                            
CURRENT   NAME                          CLUSTER      AUTHINFO           NAMESPACE
*         kubernetes-admin@kubernetes   kubernetes   kubernetes-admin   
          minikube                      minikube     minikube           default
 fire@ashutoshhs-MacBook-Air  ~/Desktop/deployapps  kubectl  get  nodes
NAME            STATUS   ROLES                  AGE   VERSION
control-plane   Ready    control-plane,master   33h   v1.22.4
node1           Ready    <none>                 33h   v1.22.4
node2           Ready    <none>                 33h   v1.22.4

```

### Namespace in k8s 

<img src="ns.png">

### list of default namespaces 

```
kubectl  get  ns
NAME              STATUS   AGE
default           Active   18m
kube-node-lease   Active   18m
kube-public       Active   18m
kube-system       Active   18m

```

### k8s internal component is running as pod 

```
 kubectl  get  po   -n kube-system  
NAME                                       READY   STATUS    RESTARTS      AGE
calico-kube-controllers-56b8f699d9-tddq6   1/1     Running   4 (17h ago)   33h
calico-node-fkc5d                          1/1     Running   3 (17h ago)   33h
calico-node-m2rht                          1/1     Running   3 (17h ago)   33h
calico-node-qjnk6                          1/1     Running   3 (17h ago)   33h
coredns-78fcd69978-ftrhb                   1/1     Running   3 (17h ago)   33h
coredns-78fcd69978-nnmtq                   1/1     Running   3 (17h ago)   33h
etcd-control-plane                         1/1     Running   3 (17h ago)   33h
kube-apiserver-control-plane               1/1     Running   3 (17h ago)   33h
kube-controller-manager-control-plane      1/1     Running   3 (17h ago)   33h
kube-proxy-bnzgf                           1/1     Running   3 (17h ago)   33h
kube-proxy-kl6mm                           1/1     Running   3 (17h ago)   33h
kube-proxy-rptk4                           1/1     Running   3 (17h ago)   33h

```

### setting namespace to default cluster 

```
 kubectl get  po
No resources found in default namespace.
 fire@ashutoshhs-MacBook-Air  ~/Desktop/deployapps  kubectl  config set-context  --current --namespace=ashu-space
Context "kubernetes-admin@kubernetes" modified.
 fire@ashutoshhs-MacBook-Air  ~/Desktop/deployapps  
 fire@ashutoshhs-MacBook-Air  ~/Desktop/deployapps  
 fire@ashutoshhs-MacBook-Air  ~/Desktop/deployapps  kubectl get  po                                              
No resources found in ashu-space namespace.
 fire@ashutoshhs-MacBook-Air  ~/Desktop/deployapps  
 fire@ashutoshhs-MacBook-Air  ~/Desktop/deployapps  
 fire@ashutoshhs-MacBook-Air  ~/Desktop/deployapps  kubectl  config get-contexts 
CURRENT   NAME                          CLUSTER      AUTHINFO           NAMESPACE
*         kubernetes-admin@kubernetes   kubernetes   kubernetes-admin   ashu-space
          minikube                      minikube     minikube           default
 fire@ashutoshhs-MacBook-Air  ~/Desktop/deployapps  
 
 ```
 
 ### building multi stage dockerfile 
 
 <img src="mult.png">
 
 
 ```
 FROM oraclelinux:8.3  as Builder
LABEL "name"="ashutoshh"
RUN dnf install java-1.8.0-openjdk.x86_64 java-1.8.0-openjdk-devel.x86_64  -y
RUN dnf install maven -y
RUN mkdir /javawebapp
WORKDIR /javawebapp
COPY . . 
# to build project into war file 
RUN mvn clean package


FROM tomcat 
MAINTAINER ashutoshh@linux.com
RUN mkdir  /myapp
COPY  --from=Builder  /javawebapp  /myapp
RUN cp -rvf  /myapp/target/WebApp.war  /usr/local/tomcat/webapps/
RUN rm -rf /myapp
EXPOSE 8080
 ```

### 

```
docker build  -t  dockerashu/ciscojavaapp:v1  https://github.com/redashu/java-springboot.git
```

## Networking in k8s 

### Node networking  (handle by Infra / network team )

### Pod networking  (k8s engg)

<img src="net1.png">



