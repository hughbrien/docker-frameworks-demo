#!/bin/bash

FROM ubuntu:14.10

MAINTAINER Deepak 

# Update the repository sources list
RUN apt-get update

################## BEGIN INSTALLATION ######################

# Install project dependencies
RUN apt-get install -y curl
RUN apt-get install -y wget
RUN apt-get install -y unzip
RUN apt-get install dos2unix

# Install MySQL Server
RUN apt-get install -y debconf-utils
RUN echo 'mysql-server mysql-server/root_password password root' | sudo debconf-set-selections 
RUN echo 'mysql-server mysql-server/root_password_again password root' | sudo debconf-set-selections 
RUN apt-get install -y mysql-server


# Install Oracle Java 7
RUN mkdir /mnt/tempdircopy
RUN cd /mnt/tempdircopy
RUN wget https://s3.amazonaws.com/appdynamics-docker-artifacts/jdk-8u5-linux-x64/jdk-8u5-linux-x64.tar.gz
RUN mkdir /opt/jdk
RUN tar -zxvf jdk-8u5-linux-x64.tar.gz -C /opt/jdk
RUN update-alternatives --install /usr/bin/java java /opt/jdk/jdk1.8.0_05/bin/java 100
RUN update-alternatives --install /usr/bin/javac javac /opt/jdk/jdk1.8.0_05/bin/javac 100
RUN update-alternatives --display java
RUN update-alternatives --display javac

# Install Tomcat Server
RUN mkdir /mnt/dockerdemo 
RUN mkdir /mnt/dockerdemo/server 
RUN mkdir /mnt/dockerdemo/server/tomcatone
RUN mkdir /mnt/dockerdemo/server/tomcattwo
RUN wget https://s3.amazonaws.com/appdynamics-docker-artifacts/apache-tomee-1.7.1-plus/apache-tomee-1.7.1-plus.tar.gz -O  /mnt/tempdircopy/apache-tomee-1.7.1-plus.tar.gz
RUN wget https://s3.amazonaws.com/appdynamics-docker-artifacts/apache-tomee-1.7.1-plus/jersy-jar.zip -O  /mnt/tempdircopy/jersy-jar.zip
RUN unzip /mnt/tempdircopy/jersy-jar.zip -d /mnt/tempdircopy/
RUN tar -zxvf /mnt/tempdircopy/apache-tomee-1.7.1-plus.tar.gz -C /mnt/tempdircopy

RUN cp -r /mnt/tempdircopy/jersy-jar/* /mnt/tempdircopy/apache-tomee-plus-1.7.1/lib/
RUN cp -r /mnt/tempdircopy/apache-tomee-plus-1.7.1/* /mnt/dockerdemo/server/tomcatone/
RUN cp -r /mnt/tempdircopy/apache-tomee-plus-1.7.1/* /mnt/dockerdemo/server/tomcattwo/

RUN wget https://s3.amazonaws.com/appdynamics-docker-artifacts/Config-sh-files/ejb/catalina1.sh -O /mnt/tempdircopy/catalina1.sh
RUN dos2unix /mnt/tempdircopy/catalina1.sh
RUN wget https://s3.amazonaws.com/appdynamics-docker-artifacts/Config-sh-files/ejb/catalina2.sh -O /mnt/tempdircopy/catalina2.sh
RUN dos2unix /mnt/tempdircopy/catalina2.sh

RUN wget https://s3.amazonaws.com/appdynamics-docker-artifacts/Config-xml-files/ejb/server2.xml -O /mnt/tempdircopy/server2.xml
RUN dos2unix /mnt/tempdircopy/server2.xml

RUN cp /mnt/tempdircopy/server2.xml  /mnt/dockerdemo/server/tomcattwo/conf/server.xml
RUN cp /mnt/tempdircopy/catalina1.sh /mnt/dockerdemo/server/tomcatone/bin/catalina.sh
RUN cp /mnt/tempdircopy/catalina2.sh /mnt/dockerdemo/server/tomcattwo/bin/catalina.sh

RUN wget https://s3.amazonaws.com/appdynamics-docker-artifacts/war-files/ejb/EJBService.war -O /mnt/tempdircopy/EJBService.war
RUN wget https://s3.amazonaws.com/appdynamics-docker-artifacts/war-files/ejb/EJBClient.war -O /mnt/tempdircopy/EJBClient.war 

RUN cp /mnt/tempdircopy/EJBClient.war  /mnt/dockerdemo/server/tomcatone/webapps/EJBClient.war 
RUN cp /mnt/tempdircopy/EJBService.war /mnt/dockerdemo/server/tomcattwo/webapps/EJBService.war

#Download java and machine agent configured controller info file
RUN wget https://s3.amazonaws.com/appdynamics-docker-artifacts/Config-xml-files/ejb/controller-info.xml -O /mnt/tempdircopy/controller-info.xml
RUN wget https://s3.amazonaws.com/appdynamics-docker-artifacts/Config-xml-files/ejb/machine-controller-info.xml -O /mnt/tempdircopy/machine-controller-info.xml

#Download script file
RUN mkdir /mnt/script
RUN wget https://s3.amazonaws.com/appdynamics-docker-artifacts/script/ejb/run.sh -O /mnt/script/run.sh
RUN dos2unix /mnt/script/run.sh
RUN chmod +x /mnt/script/run.sh

#Download SQL file
RUN wget https://s3.amazonaws.com/appdynamics-docker-artifacts/SQL+files/ejb.sql -O /mnt/tempdircopy/ejb.sql
RUN dos2unix /mnt/tempdircopy/ejb.sql
##################### INSTALLATION END #####################

 