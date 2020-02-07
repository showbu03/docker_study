# docker_study 5day

1. Container Network
1) Default network(docker0) address 변경
	# vim /etc/docker/daemon.json 
	{
	  "insecure-registries": ["10.100.0.0/24"],
	  "bip": "192.168.100.254/24"
	}
	# systemctl restart docker


2) Network Driver
 Network: bridge host ipvlan macvlan null overlay
 default : bridge(docker0)


docker run --name web -d nginx
172.17.0.2

docker run --name web -d --net=none nginx
docker run --name web -d --net=host nginx

# docker network create --driver macvlan --subnet 192.168.100.0/24   mynet


3) User Defined Network
# docker network create --driver bridge --subnet 192.168.10.0/24 --gateway 192.168.10.1 testnet
# docker run --rm -it --network testnet --ip 192.168.10.50 busybox


4) 네트워크 공유(여러컨테이너가 동일 IP address)
# docker run -d --name web  nginx
# docker run -it --name c1 --net=container:web centos


5) Port
-p hostPort:containerPort
-p containerPort
-P

	docker run -p 80:80 -p 443:443 --name web -d nginx
	docker run -p 10.100.0.105:8080:80 --name web -d nginx

		randomport:80
	docker run -p 80 --name web -d nginx
	
	
	dockerfile
	EXPOSE 8080 


		random:8080
		random:8443
	docker run -P --name web -d nginx

	docker run --expose 8080 --name web -d nginx


	

docker run -d -p 80:80 -v /webdata:/usr/share/nginx nginx

docker run -d -p 81:80 -v /webdata:/usr/share/nginx nginx

docker run -d -p 82:80 -v /webdata:/usr/share/nginx nginx


	host 80, 81, 82
	LB(nginx  www.example.com -?)




# docker run -ti --name ubu ubuntu:18.04
/ # apt-get update
/ # apt-get install iproute2 netcat-traditional inetutils-ping -y
/ # ip addr show dev eth0
/ # ip route list
/ # exit
# docker commit ubu ubuntu_net


2. Docker compose

# curl -L "https://github.com/docker/compose/releases/download/1.25.3/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

# chmod +x /usr/local/bin/docker-compose
# docker-compose --version
# docker-compose up -d


- example : docker run --name dir-web-num -p 80:80 nginx
# mkdir webserver
# cd webserver
# cat > docker-compose.yaml
version: '2'
services:
  web:
    image: nginx
    ports:
      - "80:80"


docker run --name mysql  -e MYSQL_ROOT_PASSWORD=pass mysql:latest  mysqld
docker run --name web  -p 80:80 --link mysql:db httpd:latest apachectl -DFOREGROUND

version: '3.0'
services:
  web:
    image: httpd:latest
    ports:
      - "80:80"
    links:
      - mysql:db
    command: apachectl -DFOREGROUND
  mysql:
    image: mysql:latest
    command: mysqld
    environment:
      MYSQL_ROOT_PASSWORD: pass


- example 3
cat > requirements.txt
flask
redis


version: '3'
services:
  web:
    build: .
    ports:
    - "5000:5000"
redis:
    image: "redis:alpine"
