Docker File :
	Docker file is used to generate docker image for JSF.
	This image is built with containing necessary artefacts to run JSF container.
  
Script File :
	run.sh file is used to generate load for JSF application.
	This script file is loaded under container as part of the docker image created.   
  

Steps to build docker image and Generate load for JSF application:
	1. Download Dockerfile from (url:https://github.com/Appdynamics/docker-frameworks-demo/tree/master/JSF)
	2. Build the docker image by running the command :docker build -t="appdynamics/<application name>:<tagname>" <Docker filepath>
	3. Build the container by running the command: docker run -i -t <latest generated image by docker file(image ID)> /bin/bash
	4. Navigate to the path /mnt/script to run the script file "run.sh" which generate load for JSF application
	  -> pass arguments while running run.sh file as mentioned below
	  -> ./run.sh <controller ip> <port number> ,eg:-./run.sh ec2-54-204-218-30.compute-1.amazonaws.com 80