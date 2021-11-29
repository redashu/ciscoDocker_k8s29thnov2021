## training plan 

<img src="plan.png">


### problem in app deployment 

<img src="app1.png">

### intro to hypervisor -- Virtualization concept 

<img src="vm.png">

### problem with VM --due to entire guest OS 

<img src="prob.png">

## Default OS components 

<img src="os.png">

## Containers are using host OS kernel 

<img src="k.png">

### CRE 

<img src="cre.png">

## INtro about Docker 

<img src="docker.png">

### COntainers supported by Docker 

<img src="kk.png">

### Intro to docker Desktop 

<img src="dd.png">


### Docker Desktop download for MAC 

[Download](https://hub.docker.com/editions/community/docker-ce-desktop-mac)

### Docker Desktop download for Windows 10 / 11 

[Download](https://docs.docker.com/desktop/windows/install/)


### checking docker client side 

```
docker  -v
Docker version 20.10.8, build 3967b7d

```

### Docker engine from client side 

```
docker  version 
Client:
 Cloud integration: 1.0.17
 Version:           20.10.8
 API version:       1.41
 Go version:        go1.16.6
 Git commit:        3967b7d
 Built:             Fri Jul 30 19:55:20 2021
 OS/Arch:           darwin/amd64
 Context:           default
 Experimental:      true

Server: Docker Engine - Community
 Engine:
  Version:          20.10.8
  API version:      1.41 (minimum version 1.12)
  Go version:       go1.16.6
  Git commit:       75249d8
  Built:            Fri Jul 30 19:52:31 2021
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.4.9
  GitCommit:        e25210fe30a0a703442421b0f60afac609f950a3
 runc:
  Version:          1.0.1
  GitCommit:        v1.0.1-0-g4144b63
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0


```

### Docker remote setup 

<img src="dre.png">

### Container images 

<img src="img.png">

### Intro to image registry 

<img src="reg.png">

## Docker client operations 


### searching 

```
 docker  search   python
NAME                             DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
python                           Python is an interpreted, interactive, objec…   6769      [OK]       
pypy                             PyPy is a fast, compliant alternative implem…   297       [OK]       
nikolaik/python-nodejs           Python with Node.js                             86                   [OK]
joyzoursky/python-chromedriver   Python with Chromedriver, for running automa…   60                   [OK]
arm32v7/python                   Python is an interpreted, interactive, objec…   58                   
centos/python-35-centos7         Platform for building and running Python 3.5…   39                   
hylang                           Hy is a Lisp dialect that translates express…   39        [OK]       
centos/python-36-centos7         Platform for building and running Python 3.6…   33                   
arm64v8/python                   Python is an interpreted, interactive, objec…   25             

```

### checking docker images present on Docker host 

```
 docker  images
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
[Amith@ip-172-31-90-223 ~]$ 

```

### download image from docker hub

```
  docker pull  python 
Using default tag: latest
latest: Pulling from library/python
647acf3d48c2: Extracting [================================================>  ]  52.92MB/54.93MB
b02967ef0034: Download complete 
e1ad2231829e: Download complete 
5576ce26bf1d: Download complete 
a66b7f31b095: Download complete 
05189b5b2762: Download complete 
af08e8fda0d6: Download complete 

```

### 

```
 docker  images
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
openjdk      latest    1b3756d6df61   10 days ago   471MB
python       latest    f48ea80eae5a   11 days ago   917MB
java         latest    d23bdf5b1b1b   4 years ago   643MB

```

### Image to container 

<img src="img2cont.png">
### creating first container 

```
 docker  run  --name  ashuc1 -d   alpine:latest   ping  www.google.com 
627e400b8a237a188e6ea5ab3aa0c0503bbdf98148d237a2eb9614d3f357b454
[Amith@ip-172-31-90-223 ~]$ docker  ps
CONTAINER ID   IMAGE           COMMAND                 CREATED          STATUS          PORTS     NAMES
627e400b8a23   alpine:latest   "ping www.google.com"   47 seconds ago   Up 46 seconds             ashuc1
[Amith@ip-172-31-90-223 ~]$ 

```


### list of running containers 

```
 docker  ps
CONTAINER ID   IMAGE           COMMAND                 CREATED              STATUS              PORTS     NAMES
669d3c0b9325   alpine:latest   "ping www.google.com"   10 seconds ago       Up 9 seconds                  priyankatest1
627e400b8a23   alpine:latest   "ping www.google.com"   About a minute ago   Up About a minute             ashuc1

```

### checking output / logs

```
 docker  logs  ashuc1
PING www.google.com (142.251.111.104): 56 data bytes
64 bytes from 142.251.111.104: seq=0 ttl=51 time=1.479 ms
64 bytes from 142.251.111.104: seq=1 ttl=51 time=1.504 ms
64 bytes from 142.251.111.104: seq=2 ttl=51 time=1.544 ms
64 bytes from 142.251.111.104: seq=3 ttl=51 time=1.482 ms
64 bytes from 142.251.111.104: seq=4 ttl=51 time=1.479 ms
64 bytes from 142.251.111.104: seq=5 ttl=51 time=1.

```

### starting only stopped containers in one shot 

```
 docker  ps  -f  "status=exited"
CONTAINER ID   IMAGE           COMMAND                 CREATED          STATUS                       PORTS     NAMES
55ba3f564032   alpine:latest   "ping www.google.com"   9 minutes ago    Exited (137) 5 minutes ago             manuAlpineC2
e352cb2e04ca   alpine:latest   "ping www.google.com"   9 minutes ago    Exited (137) 4 minutes ago             goutham_c1
66c797e2687c   alpine:latest   "ping www.google.com"   9 minutes ago    Exited (137) 4 minutes ago             sathyag
78586d07bef0   alpine:latest   "ping www.google.com"   9 minutes ago    Exited (137) 5 minutes ago             yogesh
f047c12e0597   alpine:latest   "ping www.google.com"   9 minutes ago    Exited (137) 6 minutes ago             subhrajyoti
02dbdcea6dce   alpine:latest   "ping www.google.com"   10 minutes ago   Exited (0) 10 minutes ago              manuAlpineC1
669d3c0b9325   alpine:latest   "ping www.google.com"   10 minutes ago   Exited (137) 5 minutes ago             priyankatest1
7f907ab3d2ba   alpine:latest   "ping www.google.com"   11 minutes ago   Exited (0) 11 minutes ago              priyanka1
627e400b8a23   alpine:latest   "ping www.google.com"   11 minutes ago   Exited (137) 5 minutes ago             ashuc1
[Amith@ip-172-31-90-223 ~]$ 
[Amith@ip-172-31-90-223 ~]$ docker  ps  -f  "status=exited"  -q
55ba3f564032
e352cb2e04ca
66c797e2687c
78586d07bef0
f047c12e0597
02dbdcea6dce
669d3c0b9325
7f907ab3d2ba
627e400b8a23
[Amith@ip-172-31-90-223 ~]$ docker  start  $(docker  ps  -f  "status=exited"  -q)
55ba3f564032
e352cb2e04ca
66c797e2687c
78586d07bef0
f047c12e0597
02dbdcea6dce
669d3c0b9325
7f907ab3d2ba
627e400b8a23
[Amith@ip-172-31-90-223 ~]$ docker  ps
CONTAINER ID   IMAGE           COMMAND                 CREATED          STATUS         PORTS     NAMES
38fcba92ee76   alpine:latest   "ping www.google.com"   8 minutes ago    Up 4 minutes             sayed_docker_demo2
55ba3f564032   alpine:latest   "ping www.google.com"   9 minutes ago    Up 7 seconds             manuAlpineC2
e352cb2e04ca   alpine:latest   "ping www.google.com"   10 minutes ago   Up 6 seconds             goutham_c1
d855aaba3d97   alpine:latest   "ping www.google.com"   10 minutes ago   Up 2 minutes             amith-alp
9f9ecd430a98   alpine:latest   "ping www.google.com"   10 minutes ago   Up 5 minutes             chandra-alpine
66c797e2687c   alpine:latest   "ping www.google.com"   10 minutes ago   Up 6 seconds             sathyag
78586d07bef0   alpine:latest   "ping www.google.com"   10 minutes ago   Up 5 seconds             yogesh
f047c12e0597   alpine:latest   "ping www.google.com"   10 minutes ago   Up 5 seconds             subhrajyoti
7425e350cda1   alpine:latest   "ping www.google.com"   10 minutes ago   Up 5 minutes             praneetha
0ce31730b503   alpine:latest   "ping www.rediff.com"   11 minutes ago   Up 5 minutes             ashwathc1
02dbdcea6dce   alpine:latest   "ping www.google.com"   11 minutes ago   Up 4 seconds             manuAlpineC1
669d3c0b9325   alpine:latest   "ping www.google.com"   11 minutes ago   Up 4 seconds             priyankatest1
7f907ab3d2ba   alpine:latest   "ping www.google.com"   12 minutes ago   Up 3 seconds             priyanka1
627e400b8a23   alpine:latest   "ping www.google.com"   12 minutes ago   Up 3 seconds             ashuc1

```

### access any running container shell 

```

[Amith@ip-172-31-90-223 ~]$ 
[Amith@ip-172-31-90-223 ~]$ docker  exec  -it  ashuc1  sh 
/ # whoami
root
/ # uname  -r
5.10.75-79.358.amzn2.x86_64
/ # exit

```

### kill all running containds 

```
 docker  kill $(docker  ps -q)
38fcba92ee76
55ba3f564032
e352cb2e04ca
9f9ecd430a98
78586d07bef0
f047c12e0597
7425e350cda1
669d3c0b9325
7f907ab3d2ba
[Amith@ip-172-31-90-223 ~]$ docker  ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

```


## removing all the dead containers 


```
docker  rm $(docker ps -aq)
38fcba92ee76
55ba3f564032
d855aaba3d97
9f9ecd430a98
78586d07bef0

```

### namespaces in docker engine for container isolation 

<img src="ns.png">

### app containerization 

<img src="appcontx.png">


### image building for any app 

<img src="appimg.png">

### python app image build

```
cd  pythonapp
[ec2-user@ip-172-31-90-223 pythonapp]$ ls
cisco.py  Dockerfile
[ec2-user@ip-172-31-90-223 pythonapp]$ docker  build  -t  ashupython:appv1  . 
Sending build context to Docker daemon  3.584kB
Step 1/7 : FROM centos
latest: Pulling from library/centos
a1d0c7532777: Extracting  79.66MB/83.52MB


```

### checking images 

```
[ec2-user@ip-172-31-90-223 pythonapp]$ docker  images
REPOSITORY        TAG       IMAGE ID       CREATED          SIZE
amithapp          v1        4c979b383a23   10 seconds ago   277MB
gopython          appv1     087bdb59e85e   10 seconds ago   277MB
chandra-python    v1        85d10f1af5d6   17 seconds ago   277MB
ashwathpython     appv1     2cf8cd59f8d3   28 seconds ago   277MB
sathyagouthampy   appv1     6e2e689fd534   31 seconds ago   277MB
ashupython        appv1     b17e3a0230f6   32 seconds ago   277MB

```

### creating python app container 

```
docker  run -it -d --name ashupyc1  ashupython:appv1 
0a5fd1ca3ede05cb15a8b97a94163281bd8fb7c7ca7ac91ff9665c78772fa77a
[ec2-user@ip-172-31-90-223 pythonapp]$ docker  ps
CONTAINER ID   IMAGE              COMMAND                  CREATED         STATUS         PORTS     NAMES
0a5fd1ca3ede   ashupython:appv1   "python3 /code/cisco…"   6 seconds ago   Up 5 seconds             ashupyc1


```

### checking stats 

```
yedfirstpyapp    0.00%     3.441MiB / 7.761GiB   0.04%     822B / 0B     0B / 0B     1
54570b3a7aa1   mithuncon1         0.00%     3.434MiB / 7.761GiB   0.04%     822B / 0B     0B / 0B     1
e5170f692504   chandra-c1         0.01%     3.438MiB / 7.761GiB   0.04%     822B / 0B     0B / 0B     1
c28c7e883e71   subhrac1           0.00%     3.43MiB / 7.761GiB    0.04%     822B / 0B     0B / 0B     1
0a5fd1ca3ede   ashupyc1           0.00%     3.445MiB / 7.761GiB   0.04%     1.04kB / 0B   0B / 0B     1
3ac845550dd4   amithpyc1          0.01%     3.426MiB / 7.761GiB   0.04%     570B / 0B     0B / 0B     1
56d78f2ccb6e   sathyagouthampyc   0.00%     3.449MiB / 7.761GiB   0.04%     500B / 0B     0B / 0B     1
^C
[ec2-user@ip-172-31-90-223 pythonapp]$ docker  stats

```

### checking live output of running container 

```
 docker logs -f ashupyc1
Hello all , welcome to python..!!
Welcome to LnB..
Welcome to Containers ..!!
______________________
Hello all , welcome to python..!!
Welcome to LnB..
Welcome to Containers ..!!

```

### if we update code we have to rebuild that image 

```
 49  docker  build  -t  ashupython:appv2  .
   50  history 
[ec2-user@ip-172-31-90-223 pythonapp]$ docker  images  |   grep  -i ashu
ashupython        appv2               1aadc6fa9a8e   23 seconds ago   277MB
ashupython        firstapp            97f1cd55dbc4   12 minutes ago   277MB
ashupython        appv1               b17e3a0230f6   16 minutes ago   277MB
[ec2-user@ip-172-31-90-223 pythonapp]$ docker run -itd --name ashupyc1 ashupython:appv2
5aaec902dc1ee1147d405bf9037a9be5de061539f3cc4ce5b1ebfb1e8b3ac22d
[ec2-user@ip-172-31-90-223 pythonapp]$ docker logs -f ashupyc1
Hello all , welcome to python..!!
Welcome to Cisco India !..
Welcome to Containers ..!!

```

### rebuild image will be cached 

```
docker  build  -t  ashupython:appv3  .
Sending build context to Docker daemon  4.608kB
Step 1/8 : FROM centos
 ---> 5d0da3dc9764
Step 2/8 : LABEL name=ashutoshh
 ---> Using cache
 ---> 695c4070a07c
Step 3/8 : LABEL email=ashutoshh@linux.com
 ---> Using cache
 ---> b353fe190108
Step 4/8 : RUN  yum install python3 -y

```

### CMD keyword inside dockerfile is replacable 

```
 63  docker run -itd --name ashuapp1  ashupython:appv3  
   64  docker ps
   65  docker run -itd --name ashuapp2  ashupython:appv3  python3 /code/test.py  
   
```

### docker containers cleaning up 

```
 docker  kill ashuapp1  ashuapp2
ashuapp1
ashuapp2
[ec2-user@ip-172-31-90-223 pythonapp]$ docker  rm  ashuapp1  ashuapp2
ashuapp1
ashuapp2

```







