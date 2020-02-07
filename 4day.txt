# docker_study 4day

1. SECURITY AND RESOURCE LIMITS
1) SECURITY

2) RESOURCE LIMITS
# docker run --name c1 -itd -m 512m ubuntu

# yum install -y epel-release && yum install -y htop
# docker run -d --name c1 --cpuset-cpus 1 smlinux/stress stress --cpu 1



# docker run -d -v /webdata:/usr/share/nginx/html:ro --name web nginx
	
docker run -v /:/tmp  centos




3) Docker Monitoring
docker top	
docker exec
docker logs
docker events
docker stats


docker run --name c1 -m 129m --memory-swap 129m -d smlinux/stress stress --vm 1  --vm-bytes 127m 
docker run -d --name c2 -m 129m  smlinux/stress stress --vm 1  --vm-bytes 200m 
docker run -d --name c3 --cpu-shares 2048   smlinux/stress:latest
docker run -d  --name c4 --cpu-shares 512  smlinux/stress:latest
docker run -d --name c5 --cpuset-cpus 1 smlinux/stress stress --cpu 1


docker run \
  --volume=/:/rootfs:ro \
  --volume=/var/run:/var/run:ro \
  --volume=/sys:/sys:ro \
  --volume=/var/lib/docker/:/var/lib/docker:ro \
  --volume=/dev/disk/:/dev/disk:ro \
  --publish=8080:8080 \
  --detach=true \
  --name=cadvisor \
  gcr.io/google-containers/cadvisor:latest



2. CONTAINER STORAGE

1) volume mount
-v <컨테이너 마운드 경로>
-v <호스트 경로>:<컨테이너 마운드 경로>
-v <호스트 경로>:<컨테이너 마운드 경로>:<읽기 쓰기 모드>


docker run -v /webdata:/usr/share/nginx/html --name web -d nginx
mkdir /webdata
$ docker run -v /webdata:/usr/share/nginx/html:ro --name web -d nginx


	/var/lib/docker/volumes/UUID/_data:/usr/share/nginx/html
docker run -v /usr/share/nginx/html --name web -d nginx


	dockerfile
	...
	VOLUME ["/var/lib/registry"]
	...

	/var/lib/docker/volumes/UUID/_data:/var/lib/registry
$ docker run --name reg -d registry


$ docker volume create webdata
$ docker run -v webdata:/usr/share/nginx/html:ro --name web -d nginx


$ docker run -v dbdata:/var/lib/mysql -d -e MYSQL_ROOT_PASSWORD=pass --name db mysql

$ touch ubuntu_history
$ docker run -it -v /root/ubuntu_history:/root/.bash_history ubuntu 





	generator:latest		 nginx
		|			  |
		+-- /htdocs/index.html	  +-- /usr/share/nginx/html

	---------------------------------------
		       /webdata/index.html
		

	docker run --name gen -v /webdata:/htdocs -d generator
	docker run --name web -v /webdata:/usr/share/nginx/html -d nginx


	
	dataonly(busybox)		db(mysql)
		|				| --volumes-from dataonly
		+-- /var/lib/mysql <------------+

	docker run -it --name dataonly -v data:/var/lib/mysql -v web:/usr/share/nginx/html busybox
	docker run -d -e MYSQL_ROOT_PASSWORD=pass  --volumes-from dataonly --name db mysql


	/var/lib/docker/volumes/data



docker.example.com -- disk(/dev/vda, /dev/vdb:100G)
/var/lib/docker/ : /dev/vdb

backup
# systemctl stop docker
# tar cf /docker.tar  /var/lib/docker



		[----50G docker]
	storage[-----------------------------100G]
# pvcreate /dev/vdb
# vgcreate storage /dev/vdb

# lvcreate -L 50G --name docker storage
format
# mkfs -t xfs /dev/storage/docker

# vim /etc/fstab
...
/dev/storage/docker  /var/lib/docker  xfs  defaults  0 0

# mount -a

# cd / 
# tar xf docker.tar
# systemctl start docker


# docker ps


$ docker volume create --driver local \
    --opt type=nfs \
    --opt o=addr=10.100.0.254 \
    --opt device=:/container/webdata \
    webdata
