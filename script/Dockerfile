FROM ubuntu
LABEL email=ashutoshh@linux.com
RUN mkdir /code 
COPY data.sh /code/data.sh 
WORKDIR /code
RUN chmod +x data.sh 
# making script executable 
ENTRYPOINT ["./data.sh"]
# Replacement of CMD 