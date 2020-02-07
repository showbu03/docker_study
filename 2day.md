# docker_study 2day

1. docker commands

1) 컨테이너 이미지 관리
	filesystem : UFS
	-이미지 검색 : docker search key_word
	- 이미지 다운로드 : docker image pull  == docker pull nginx
	- 이미지 삭제 : docker image rm	== docker rmi
	- 이미지 목록보기 : docker image ls	== docker images
	-이미지 구조를 확인:  docker image inspect 

2) container 관리

	run 
		local host 찾기
		pull -> create -> start -> attach

	docker run -it ubuntu:latest 

	/# 
	docker run -d nginx 

	# docker ps
	# docker ps -a


	# docker rm -f $(docker ps -aq)
	# alias crm='docker rm -f $(docker ps -aq)'
	# vim ~/.bashrc

	• 컨테이너 생성 : docker container create  == docker create
	• 컨테이너 생성 및 구동 : docker container run  == docker run
	• 컨테이너 구동 : docker container start  == docker start 
	• 컨테이너 중지 : docker container stop  == docker stop
	• 컨테이너 삭제 : docker container rm  == docker rm 
	• 컨테이너 목록 확인 : docker container ps == docker ps 


	# docker create -it ubuntu
	$ docker start xxxxx
	/# apt-get update
	/# apt-get install iproute2 -y
	/# rm /bin/fgrep
	/# echo "#" >> .bashrc
	/# ps -ef
	PID1=/bin/bash
	/# exit			or Ctrl +p,q

	$ docker inspect c1

	Runtime mode - detached와 foreground
	# docker run --name web1 -d nginx:latest 

	# docker inspect web1

	• 컨테이너의 접속: docker container attach
	• 컨테이너 이름 변경 : docker container rename
	• 컨테이너 내에서 파일 변경이력 확인 : docker container diff
	• 컨테이너의 표준 출력 결과 보기: docker container logs

	• 컨테이너 프로세스 실행 : docker container exec
	• 컨테이너 프로세스 정보보기 : docker container top
	• 컨테이너 내에서 파일 복사 : docker container cp
	• 컨테이너 내에서 파일 변경이력 확인 : docker container diff


	$ docker exec -it web1 /bin/bash
	/# cd /usr/share/nginx/html/
	/# echo "HPE" > index.html 

	$ docker cp web1:/usr/share/nginx/html/index.html  .
	$ docker cp index.html web1:/usr/share/nginx/html/index.html

	- commit
	docker commit c1 myubuntu:20200204


	- export and import

	$ wget ftp://59.29.224.87/pub/my.tar

	# docker cp index.html web1:/usr/share/nginx/html/index.html


	alias cip='docker inspect -f "{{.NetworkSettings.IPAddress}}"'


	docker run --name daemon_test -d ubuntu /bin/sh -c "while true; do date; sleep 3; done"


	docker run -it --name cowsay --hostname cowsay debian:latest /bin/bash
	/#

- volume mount
# mkdir /webdata
# cd /webdata/
# echo "hpe" > index.html
docker run -d --name web 

docker run --name db -e MYSQL_ROOT_PASSWORD=pass -d -v /dbdata:/var/lib/mysql mysql


2. Container Registry

- public registry(hub.docker.com)
	{repositoryName}:{tag}
	{namespace}/{repositoryName}:{tag}
	ubuntu:18.04		smlinux/myubuntu:20200204
	ubuntu:16.04
	ubuntu:19.10
	ubuntu:20.04
	busybox

	$ docker login
	$ docker push smlinux/myubuntu:20200204

# mkdir exam
# cde exam
# wget ftp://59.29.224.87/pub/docker/*
# chmod +x dockertags



- private registry(사내에서 운영하는  registry:master.example.com)
{registryAddress}/{repositoryName}:{tag}
	master.example.com:5000/ubuntu:16.04
	10.100.0.104:5000/ubuntu:19.10

$ docker run -d -p 5000:5000  -v /registry:/var/lib/registry --restart always --name registry registry:2

$ docker pull ubuntu
$ docker tag ubuntu localhost:5000/ubuntu
docker$ docker push master.example.com:/ubuntu

----
lab 3
/root/registry_data		##/var/lib/regisry
	|
	+--- containers...

/root/nginx_data		## NGINX'S /etc/nginx/conf.d/
	|
	+--- registry.password(smlee/work)
	+--- server-nginx.crt
	+--- server-nginx.key
	+--- registry.conf



# mkdir -p /root/registry_data
# mkdir -p /root/nginx_data
# cd /root/nginx_data
# docker run -d -v /root/registry_data:/var/lib/registry --name registry registry
# yum install httpd-tools -y
# htpasswd -c registry.password smlee



# wget ftp://59.29.224.87/pub/docker/registry.conf
# cat registry.conf

upstream docker-registry {
  server registry:5000;
}
server {
  listen 443;
  server_name 10.100.0.104;
  # SSL
  ssl on;
  ssl_certificate /etc/nginx/conf.d/server-nginx.crt;
  ssl_certificate_key /etc/nginx/conf.d/server-nginx.key;
...


# openssl genrsa -out client-crt-key.key 2048
# openssl req -x509 -new -nodes -key client-crt-key.key -days 10000 -out client-crt.crt

# openssl genrsa -out server-nginx.key 2048
# openssl req -new -key server-nginx.key -out my-registry.csr
   Common Name (eg, your name or your server's hostname) []: master.example.com

# echo subjectAltName = IP:10.100.0.104,IP:127.0.0.1,DNS:master.example.com > extfile.cnf
# openssl x509 -req -in my-registry.csr -CA client-crt.crt -CAkey client-crt-key.key -CAcreateserial -out server-nginx.crt -days 10000 -extfile extfile.cnf

# cp client-crt.crt /etc/pki/ca-trust/source/anchors/client-crt.pem
# update-ca-trust


# mv /etc/docker/daemon.json /tmp
# systemctl stop docker
# systemctl start docker

# docker start registry

# docker run -d -p 443:443 --link registry:registry -v /root/nginx_data:/etc/nginx/conf.d --name nginx nginx:1.9

# docker login https://10.100.0.104
Username: smlee
Password: work

# cat ~/.docker/config.json

# docker login https://master.example.com


test
# docker tag busybox:latest master.example.com/busybox:v1
# docker push master.example.com/busybox:v1
# docker rmi master.example.com/busybox:v1
# docker rmi busybox
# docker pull master.example.com/busybox:v1

====docker.example.com
# scp client-crt.crt docker.example.com:~
# cp client-crt.crt /etc/pki/ca-trust/source/anchors/client-crt.pem
# update-ca-trust
# mv /etc/docker/daemon.json /tmp
# systemctl stop docker
# systemctl start docker

# docker login https://master.example.com

# docker pull master.example.com/busybox:v1
