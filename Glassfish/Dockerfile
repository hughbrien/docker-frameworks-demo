#!/bin/bash

FROM ubuntu:14.10

MAINTAINER Udaya Narayanachar 

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


# Install GlassFish Server
RUN cd /mnt/tempdircopy 
RUN wget https://s3.amazonaws.com/appdynamics-docker-artifacts/glassfish-4.0/glassfish-4.0.zip -O /mnt/tempdircopy/glassfish.zip
RUN unzip /mnt/tempdircopy/glassfish.zip -d /opt
RUN export PATH=/opt/glassfish4/bin:$PATH
RUN wget https://s3.amazonaws.com/appdynamics-docker-artifacts/Config-xml-files/glassfish/domain.xml -O /opt/glassfish4/glassfish/domains/domain1/config/domain.xml
RUN wget https://s3.amazonaws.com/appdynamics-docker-artifacts/Config-properties-files/glassfish/config.properties -O /mnt/tempdircopy/config.properties
RUN cp /mnt/tempdircopy/config.properties  /opt/glassfish4/glassfish/osgi/felix/conf/config.properties
RUN wget https://s3.amazonaws.com/appdynamics-docker-artifacts/war-files/glassfish/GlassFishClient.war -O /mnt/tempdircopy/GlassFishClient.war


# Install Tomcat Server
RUN mkdir /mnt/dockerdemo 
RUN mkdir /mnt/dockerdemo/server 
RUN mkdir /mnt/dockerdemo/server/tomcat
RUN wget https://s3.amazonaws.com/appdynamics-docker-artifacts/apache-tomcat-7.0.55/apache-tomcat-7.0.55.tar.gz -O  /mnt/tempdircopy/apache-tomcat-7.0.55.tar.gz
RUN tar -zxvf /mnt/tempdircopy/apache-tomcat-7.0.55.tar.gz -C /mnt/tempdircopy
RUN cp -r /mnt/tempdircopy/apache-tomcat-7.0.55/* /mnt/dockerdemo/server/tomcat
RUN wget https://s3.amazonaws.com/appdynamics-docker-artifacts/Config-sh-files/glassfish/catalina2.sh -O /mnt/tempdircopy/catalina.sh
RUN dos2unix /mnt/tempdircopy/catalina.sh
RUN wget https://s3.amazonaws.com/appdynamics-docker-artifacts/Config-xml-files/glassfish/server2.xml -O /mnt/tempdircopy/server.xml
RUN dos2unix /mnt/tempdircopy/server.xml
RUN cp /mnt/tempdircopy/server.xml /mnt/dockerdemo/server/tomcat/conf/server.xml
RUN cp /mnt/tempdircopy/catalina.sh /mnt/dockerdemo/server/tomcat/bin/catalina.sh

RUN wget https://s3.amazonaws.com/appdynamics-docker-artifacts/war-files/glassfish/GlassFishService.war -O /mnt/tempdircopy/GlassFishService.war
RUN cp /mnt/tempdircopy/GlassFishService.war /mnt/dockerdemo/server/tomcat/webapps/GlassFishService.war

#Download java and machine agent configured controller info file
RUN wget https://s3.amazonaws.com/appdynamics-docker-artifacts/Config-xml-files/glassfish/controller-info.xml -O /mnt/tempdircopy/controller-info.xml
RUN wget https://s3.amazonaws.com/appdynamics-docker-artifacts/Config-xml-files/glassfish/machine-controller-info.xml -O /mnt/tempdircopy/machine-controller-info.xml

#Download script file
RUN mkdir /mnt/script
RUN wget https://s3.amazonaws.com/appdynamics-docker-artifacts/script/glassfish/run.sh -O /mnt/script/run.sh
RUN dos2unix /mnt/script/run.sh
RUN chmod +x /mnt/script/run.sh

#Download SQL file
RUN wget https://s3.amazonaws.com/appdynamics-docker-artifacts/SQL+files/glassfish.sql -O /mnt/tempdircopy/glassfish.sql
RUN dos2unix /mnt/tempdircopy/glassfish.sql
##################### INSTALLATION END #####################