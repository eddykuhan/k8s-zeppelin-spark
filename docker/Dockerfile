
# Pull base image  
FROM ubuntu:16.04
  
MAINTAINER eddykuhan "eddykuhan92@gmail.com"
  
# update source
RUN echo "deb http://archive.ubuntu.com/ubuntu/ trusty main restricted" > /etc/apt/sources.list && \
    echo "deb-src http://archive.ubuntu.com/ubuntu/ trusty main restricted " >> /etc/apt/sources.list && \
    echo "deb http://archive.ubuntu.com/ubuntu/ trusty-updates main restricted " >> /etc/apt/sources.list && \
    echo "deb-src http://archive.ubuntu.com/ubuntu/ trusty-updates main restricted " >> /etc/apt/sources.list && \
    echo "deb http://archive.ubuntu.com/ubuntu/ trusty universe " >> /etc/apt/sources.list && \
    echo "deb-src http://archive.ubuntu.com/ubuntu/ trusty universe " >> /etc/apt/sources.list && \
    echo "deb http://archive.ubuntu.com/ubuntu/ trusty-updates universe " >> /etc/apt/sources.list && \
    echo "deb-src http://archive.ubuntu.com/ubuntu/ trusty-updates universe " >> /etc/apt/sources.list && \
    echo "deb http://archive.ubuntu.com/ubuntu/ trusty-security main restricted " >> /etc/apt/sources.list && \
    echo "deb-src http://archive.ubuntu.com/ubuntu/ trusty-security main restricted " >> /etc/apt/sources.list && \
    echo "deb http://archive.ubuntu.com/ubuntu/ trusty-security universe " >> /etc/apt/sources.list && \
    echo "deb-src http://archive.ubuntu.com/ubuntu/ trusty-security universe ">> /etc/apt/sources.list &&\
    apt-get update
  
# Install curl  nano wget
RUN apt-get -y install curl nano wget
#RUN curl https://bootstrap.pypa.io/get-pip.py >> get-pip.py &&\
#    python get-pip.py
#RUN pip install matplotlib -i https://pypi.tuna.tsinghua.edu.cn/simple


###########################################################################################
###### Install JDK(9)
###########################################################################################
ENV JAVA_HOME /opt/java
RUN cd /tmp && \
    curl -L 'http://download.oracle.com/otn-pub/java/jdk/8u131-b11/d54c1d3a095b4ff2b6607d096fa80163/jdk-8u131-linux-x64.tar.gz' \
         -H 'Cookie: oraclelicense=accept-securebackup-cookie; gpw_e24=Dockerfile' | tar -zx
#ADD jdk1.8.0_121.tar.gz /tmp/
RUN mkdir -p /opt
RUN mv /tmp/jdk* ${JAVA_HOME}

ENV PATH ${JAVA_HOME}/bin:$PATH



###########################################################################################
###### Install Spark(2.4.4)
###########################################################################################
ENV SPARK_HOME /opt/spark
RUN cd /tmp && \
   curl https://mirrors.tuna.tsinghua.edu.cn/apache/spark/spark-2.4.6/spark-2.4.6-bin-hadoop2.7.tgz | \
         tar -zx
#ADD spark-2.4.6-bin-hadoop2.7.tgz /tmp/
RUN mv /tmp/spark-2.4.6-bin-hadoop2.7 ${SPARK_HOME}

ENV PATH ${SPARK_HOME}/bin:$PATH



###########################################################################################
###### Install Zeppelin(0.7.3)
###########################################################################################
ENV ZEPPELIN_HOME /opt/zeppelin
RUN cd /tmp && \
    curl https://mirrors.tuna.tsinghua.edu.cn/apache/zeppelin/zeppelin-0.8.2/zeppelin-0.8.2-bin-all.tgz | \
         tar -zx
#ADD zeppelin-0.8.2-bin-all.tgz /tmp/
RUN mv /tmp/zeppelin-0.8.2-bin-all ${ZEPPELIN_HOME}
COPY zeppelin-site.xml ${ZEPPELIN_HOME}/conf/zeppelin-site.xml
COPY zeppelin-env.sh ${ZEPPELIN_HOME}/conf/zeppelin-env.sh

EXPOSE 8089


WORKDIR $ZEPPELIN_HOME
CMD bin/zeppelin.sh

