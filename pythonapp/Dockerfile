FROM centos
# centos is popular linux distro
LABEL name=ashutoshh
LABEL email=ashutoshh@linux.com 
# optional keyword but it just to store 
# info about image designer 
RUN  yum install python3 -y 
# here RUN is giving shell where we can type
# instruction 
RUN mkdir /code 
# creating folder to store our code 
COPY cisco.py /code/cisco.py 
COPY test.py /code/test.py 
# copy will be used to copy data from 
#  docker client to docker engine 
# during image build time
ENTRYPOINT  ["python3"] 
CMD ["/code/cisco.py"]
# ENTRYPOint can't be remove as argument during container creation time 
#CMD  ["python3","/code/cisco.py"]
# usage of CMD is to decide default parent proces
# of docker image 
# CMD argument can be replaced by user during container creation time 
# CMD is replacelable by user during container creation time 