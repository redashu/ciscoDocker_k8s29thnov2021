FROM openjdk
# default official jdk image 
LABEL email=ashutoshh@linux.com
RUN mkdir /codedata 
ADD cisco.java /codedata/cisco.java 
# copy and add both are same but ADD can also data from URL 
# ADD https://raw.githubusercontent.com/redashu/javaLang/main/test.java /cisco/
WORKDIR  /codedata
# is to change direcotry during image build time 
RUN javac cisco.java 
# it will compile code and store it into current directory (/codedata)
CMD ["java","myclass"]
# default parameter to set default process 