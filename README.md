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

