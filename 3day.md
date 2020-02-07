# docker_study 3day


1. DOCKERFILE
	$ mkdir build
	$ cd build
	$ ls 
	index.html abc.html xyz.html
	conf -- httpd.conf, 
	$ cat > Dockerfile
	FROM centos:7
	RUN yum install -y httpd 
	LABEL description="This is my  multiline description of the software.\
	      date="2020.2.5"
	ENV  NAME lee
	ARG  memory=1024
	WORKDIR /tmp/
	COPY index.html  .
	ADD a.tar.gz /tmp/			## /tmp/xxxx
	ADD ftp://59.29.224.87/pub/a.txt /tmp/
	RUN uaseradd -s nologinapache 
	USER apache

	EXPOSE 80 443/tcp
	CMD ["/usr/sbin/httpd", "-DFOREGROUND"]


	$ docker build  -t testweb:v1  .

	docker run testweb:v1


	$ docker run  PID1=
	FROM ubuntu:18.04
	RUN apt-get update \
	    && apt-get install -y apache2


	docker run -d --name db  -v /dbdata:/var/lib/mysql mysql



	VOLUME /var/lib/mysql

		-v /var/lib/docker/volumes/UUID/_data:/var/lib/mysql
	docker run -d --name db  mysql




	ONBUILD : 빌드된 컨테이너를 base image로 사용할때 실행되는 dockerfile의 구문

		FROM busybox
		RUN touch /a.txt
		ONBUILD RUN touch /b.txt


		docker build -t base:v1 .  	##  /a.txt


		FROM base:v1
		...


		docker build -t test:v8 .  	##  /a.txt  b.txt





	FROM ubuntu:14.04

	RUN date > /MountPointDemo/date.txt
	RUN cat /MountPointDemo/date.txt
	VOLUME /MountPointDemo


	html-generator.sh
	#!/bin/bash
	mkdir /htdocs
	while :
	  do
	  /usr/games/fortune > /htdocs/index.html
	  sleep 10
	done


	FROM debian:latest
	RUN apt-get update&& apt-get install -y fortune
	ADD html-generator.sh /bin/html-generator.sh
	RUN chmod +x /bin/html-generator.sh
	ENTRYPOINT /bin/html-generator.sh


	docker run -d --name generator -v /webdata:/htdocs generator:latest

	docker -v /webdata:/usr/share/nginx/html -p 80:80 -d --name web nginx
