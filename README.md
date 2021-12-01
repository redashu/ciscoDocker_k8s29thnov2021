## training plan 

<img src="plan.png">

### Summary of docker 

<img src="dockersum.png">

### Container registry options 

<img src="reg.png">

### Container storage need 

<img src="st1.png">

### Docker volume 

<img src="dockervol.png">

### generating docker image for data generation 

```
s]$ ls
javaapp  project-website-template  pythonapp  script
[ec2-user@ip-172-31-90-223 appimages]$ cd  script/
[ec2-user@ip-172-31-90-223 script]$ ls
data.sh  Dockerfile
[ec2-user@ip-172-31-90-223 script]$ docker  build -t  dockerashu/script:genv1 . 
Sending build context to Docker daemon  3.072kB
Step 1/7 : FROM ubuntu
 ---> ba6acccedd29
Step 2/7 : LABEL email=ashutoshh@linux.com
 ---> Running in ade2e010a7db
Removing intermediate container ade2e010a7db
 ---> 0b78c2e8d63a
 
 ```
### testing container 

```
 docker run -itd --name ashuc1  dockerashu/script:genv1 
acff78ff95e2287f3d0f1ff80a8bc052def80b2dc03dd4681d9d670b3f457f27
[ec2-user@ip-172-31-90-223 script]$ docker  ps
CONTAINER ID   IMAGE                     COMMAND       CREATED         STATUS         PORTS     NAMES
acff78ff95e2   dockerashu/script:genv1   "./data.sh"   3 seconds ago   Up 2 seconds             ashuc1
a7d953949185   chandra-script            "./data.sh"   3 seconds ago   Up 2 seconds             chandra-c1
[ec2-user@ip-172-31-90-223 script]$ docker exec -it  ashuc1  bash 
root@acff78ff95e2:/code# cd  /tmp/
root@acff78ff95e2:/tmp# ls
cisco.txt
root@acff78ff95e2:/tmp# cat  cisco.txt 
Hello Cisco this is my data ..
Hello Cisco this is my data ..
Hello Cisco this is my data ..
Hello Cisco this is my data ..
Hello Cisco this is my data ..
root@acff78ff95e2:/tmp# cat  cisco.txt 
Hello Cisco this is my data ..
Hello Cisco this is my data ..
Hello Cisco this is my data ..
Hello Cisco this is my data ..
Hello Cisco this is my data ..
Hello Cisco this is my data ..

```

### docker volume creation 

```
356  docker  volume    create   ashuvol1 
  357  docker  volume  ls
  358  docker  volume rm  e9a6812a347f1617658e289fb46deb5b3435c06f7941946a23dd7405df53c7f6 cff2eca4ddeeb73530fd67d60a0c063039ffc4530848a22cfac99ab4a6ab5036 a8c3cc7e5782dabe947fd7ca6fac58c603fd364f42f533bee3fc8fe497cbb384
  359  history 
[ec2-user@ip-172-31-90-223 script]$ docker  volume  lsDRIVER    VOLUME NAME
local     ashuvol1
local     go_vol1
local     priyankavol1
local     subhravol1
[ec2-user@ip-172-31-90-223 script]$ docker volume  inspect  ashuvol1
[
    {
        "CreatedAt": "2021-12-01T04:59:00Z",
        "Driver": "local",
        "Labels": {},
        "Mountpoint": "/var/lib/docker/volumes/ashuvol1/_data",
        "Name": "ashuvol1",
        "Options": {},
        "Scope": "local"
    }
]

```

### creating container with volume 

```
docker run -itd --name ashuc1   -v  ashuvol1:/tmp:rw      dockerashu/script:genv1
702517605ae83013ab0091a76586f1aceedd13a732ac2964198a4c1db9088248

```

#### checking data in docker engine from backend 

```
[ec2-user@ip-172-31-90-223 ~]$ sudo -i
[root@ip-172-31-90-223 ~]# cd  /var/lib/docker/
[root@ip-172-31-90-223 docker]# ls
buildkit  containers  image  network  overlay2  plugins  runtimes  swarm  tmp  trust  volumes
[root@ip-172-31-90-223 docker]# cd  volumes/
[root@ip-172-31-90-223 volumes]# ls
amith_vol  ashwathv1          chandra-volume  m1vol1       msn        priyankavol1  sayedvol1
ashuvol1   backingFsBlockDev  go_vol1         metadata.db  pranivol1  sathyav1      subhravol1
[root@ip-172-31-90-223 volumes]# cd  ashuvol1/
[root@ip-172-31-90-223 ashuvol1]# ls
_data
[root@ip-172-31-90-223 ashuvol1]# cd  _data/
[root@ip-172-31-90-223 _data]# ls
cisco.txt
[root@ip-172-31-90-223 _data]# cat  cisco.txt 
Hello Cisco this is my data ..
Hello Cisco this is my data ..
Hello Cisco this is my data ..
Hello Cisco this is my data ..
Hello Cisco this is my data ..
Hello Cisco this is my data .

```

### single volume can be part of diff containers

```
 docker  run -it --rm  -v   ashuvol1:/checkdata:ro  alpine  sh 
/ # 
/ # 
/ # cd  /checkdata/
/checkdata # ls
cisco.txt
/checkdata # rm cisco.txt 
rm: remove 'cisco.txt'? y
rm: can't remove 'cisco.txt': Read-only file system
/checkdata # cat  cisco.txt 
Hello Cisco this is my data ..
Hello Cisco this is my data ..

```

### any custom location from docker host as volume 

```
docker  run -d --name ashuweb -p 1188:80 -v /home/ec2-user/appimages/project-website-template:/usr/share/nginx/html:ro  nginx

```
### remove volumes 

```
ec2-user@ip-172-31-90-223 pythonapp]$ docker volume  ls
[ec2-user@ip-172-31-90-223 pythonapp]$ docker volume  prune 
WARNING! This will remove all local volumes not used by at least one container.
Are you sure you want to continue? [y/N] y
Deleted Volumes:
msn
sathyav1
m1vol1
chandra-volume
sayedvol1

```



