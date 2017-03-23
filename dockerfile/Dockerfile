######################################
#Docker File to install rabbitmq and configure queue system
# 
#####################################

#Starting with Base image ubuntu which has git and some basic softwares required.
FROM dipinthomas2003/ubuntu-apache:git

#Label
LABEL "Author"="Dipin Thomas"

#Working Director
WORKDIR /home

#Installing python
RUN apt-get install -y python \

#Install pika python module
	&& apt-get install python-pika 


#Updating apt repository to install rabbitmq
RUN echo "deb http://www.rabbitmq.com/debian/ testing main" >> /etc/apt/sources.list \

#Installing Curl
	&& apt-get install curl \

#Downloading Key
	&&  curl http://www.rabbitmq.com/rabbitmq-signing-key-public.asc |  apt-key add -  \

#Updating the system to latest Repo
	&& apt-get update \

#installing Rabbitmq Server
	&&  apt-get -y --allow-unauthenticated install rabbitmq-server \

#Enabing the management plugin for web management
#After below step "http://localhost:15672/" should return login page
 	&&  rabbitmq-plugins enable rabbitmq_management\

#Restart rabbitmq server
	&& /etc/init.d/rabbitmq-server restart \

#Enable Stomp Plugin	
	&& rabbitmq-plugins enable rabbitmq_web_stomp 

#Enable guest user login from network
RUN echo "[{rabbit, [{loopback_users, []}]}]." >> /etc/rabbitmq/rabbitmq.config


#Pull publisher from git repo
RUN  git clone https://github.com/dipinthomas/docker-rabbitmq.git


#exposing the ports
EXPOSE 	15670 \
	15672 \
	15674


#Start the service
CMD service rabbitmq-server start && bash
