FROM ubuntu:15.04
MAINTAINER Vinh Tran, https://github.com/vinhtran2905

#Install Java
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y  software-properties-common && \
    add-apt-repository ppa:webupd8team/java -y && \
    apt-get update && \
    echo oracle-java7-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections && \
    apt-get install -y oracle-java7-installer && \
    apt-get clean

#Install tomcat
RUN mkdir -p /opt/tomcat \
    && curl -SL http://apache.fastbull.org/tomcat/tomcat-7/v7.0.72/bin/apache-tomcat-7.0.72.tar.gz \
    | tar -xzC /opt/tomcat --strip-components=1 \
    && rm -Rf /opt/tomcat/webapps/docs /opt/tomcat/webapps/examples

COPY tomcat-users.xml /opt/tomcat/conf/

#expose tomcat
EXPOSE 8080

ENV JAVA_OPTS -server -XX:+DisableExplicitGC -XX:+UseConcMarkSweepGC \
    -XMs1G -Xmx2G -XX:Permsize=1G --XX:MaxPermSize=2G

WORKDIR /opt/tomcat 
CMD ["bin/catalina.sh","run"]
