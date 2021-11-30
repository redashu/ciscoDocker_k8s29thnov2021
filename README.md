## training plan 

<img src="plan.png">

### DMA -- Dynamic memory allocation -- Cgroups 

<img src="cg.png">

### implementing cgroups in container 

```
22  docker run -d --name ashupyc2     --memory 200m      847b4522ef83
  123  docker run -d --name ashupyc3  --cpu-shares=20     --memory 200m      847b4522ef83
```

### restart policy in docker for auto starting container 

<img src="restart.png">

### list of restart policy 

<img src="list.png">

### checking restart policy of your container 

```
docker  inspect  ashupyc3  --format='{{.HostConfig.RestartPolicy.Name}}'
```

### assign restart policy to container 

```
docker run -itd --name mec1  --restart always  alpine ping fb.com 
eabd96b9997cfc10811d768a64f0bccb9f860d5d66c7dba4a4d8e70d3ce5ee27
[ec2-user@ip-172-31-90-223 appimages]$ 
[ec2-user@ip-172-31-90-223 appimages]$ 
[ec2-user@ip-172-31-90-223 appimages]$ 
[ec2-user@ip-172-31-90-223 appimages]$ docker  inspect  mec1  --format='{{.HostConfig.RestartPolicy.Name}}'
always

```

### dockerfile for Java sample code 

### building image 
```
docker  build -t  ashujava:codev1 . 
Sending build context to Docker daemon  3.072kB
Step 1/7 : FROM openjdk
 ---> 1b3756d6df61
Step 2/7 : LABEL email=ashutoshh@linux.com
 ---> Running in 6167abc67ae1
Removing intermediate container 6167abc67ae1
 ---> 2dda1342f0f2
Step 3/7 : RUN mkdir /codedata
 ---> Running in fc6cd8ab4661
Removing intermediate container fc6cd8ab4661
 ---> cb6fac361ea8
Step 4/7 : ADD cisco.java /codedata/cisco.java
 ---> 7dfbf9c06019
Step 5/7 : WORKDIR  /codedata
 ---> Running in a15433e31606
Removing intermediate container a15433e31606
 ---> 5c6d33d5b9d1
Step 6/7 : RUN javac cisco.java
 ---> Running in 9a6a46f0eb81
Removing intermediate container 9a6a46f0eb81
 ---> 28b20ee1b86e
Step 7/7 : CMD ["java","myclass"]
 ---> Running in 7a7aa3763f5d
Removing intermediate container 7a7aa3763f5d
 ---> 157aa0aaa81c
Successfully built 157aa0aaa81c
Successfully tagged ashujava:codev1

```

### java container 
```
143  docker  run -itd --name ashuj1 ashujava:codev1
  144  docker logs -f  ashuj1
 
```

### checking internal details of container 

```
docker  exec -it  ashuj1  bash 
bash-4.4# 
bash-4.4# java -version 
openjdk version "17.0.1" 2021-10-19
OpenJDK Runtime Environment (build 17.0.1+12-39)
OpenJDK 64-Bit Server VM (build 17.0.1+12-39, mixed mode, sharing)
bash-4.4# uname -r
5.10.75-79.358.amzn2.x86_64
bash-4.4# cat  /etc/os-release 
NAME="Oracle Linux Server"
VERSION="8.5"
ID="ol"

```

### building image from custom dockerfile name 

```
 ls
cisco.java  customjdk.dockerfile  Dockerfile
[ec2-user@ip-172-31-90-223 javaapp]$ docker  build -t ashujava:codev2 -f customjdk.dockerfile .


```

### webapp containerization 

<img src="appcont.png">

### frontend app with nginx web server 

<img src="nginx.png">

### sample github html project containerization 

```
git clone  https://github.com/yenchiah/project-website-template
Cloning into 'project-website-template'...
remote: Enumerating objects: 937, done.
remote: Total 937 (delta 0), reused 0 (delta 0), pack-reused 937
Receiving objects: 100% (937/937), 1.07 MiB | 15.83 MiB/s, done.
Resolving deltas: 100% (585/585), done.


```

### building image 

```
 cd  project-website-template/
[ec2-user@ip-172-31-90-223 project-website-template]$ ls
css         embedding.html  img         js       menu.html  vid
Dockerfile  empty.html      index.html  LICENSE  README.md  widgets.html
[ec2-user@ip-172-31-90-223 project-website-template]$ docker  build -t  ciscowebapp:30novv1  . 
Sending build context to Docker daemon  1.004MB
Step 1/3 : FROM nginx
latest: Pulling from library/nginx
eff15d958d66: Pulling fs layer 
1e5351450a59: Pulling fs layer 
2df63e6ce2be: Pulling fs layer 

```

### creating container 

```
docker  run -d --name ashuc1  -p  5566:80  ciscowebapp:30novv1
6b48d849ad6d73f76991d40e3ebcac4490180985341704cb3bc71f84872216f6
[ec2-user@ip-172-31-90-223 project-website-template]$ docker  ps
CONTAINER ID   IMAGE                 COMMAND                  CREATED          STATUS          PORTS                                   NAMES
6b48d849ad6d   ciscowebapp:30novv1   "/docker-entrypoint.…"   17 seconds ago   Up 16 seconds   0.0.0.0:5566->80/tcp, :::5566->80/tcp   ashuc1

```






