Cahpter 1. CONTAINER TECHNOLOGY OVERVIEW
==========================================

베어메탈 환경
>리소스 효율성을 위해 한 서버위에 여러 어플리케이션을 올려서 사용하였고, app<->app, app<->os간 영향을 받아 파티션을 격리하기 시작함

가상화 환경
> x86 H/W 가격, 리눅스 환경 안정성 향상등 호재 겹침. 이젠 파티션을 안나누고, 하이퍼바이저를 활용해서 서버가 여러대가 있는것처럼 리소스를 나눠서 사용하기 시작함. 
> 운영하는 서버의 수가 계속 증가하기 시작함.


컨테이너 환경
> 시장의 니즈가 개인화에 맞춰 다양한 서비스로 빠르게 변화되길 원함
(50만개의 신발에서 50만가지의 신발을 만는것으로)
> 가상화 환경도 불가능한것은 아니다. AWS에서 신규 서버를 만드는데 1~2분 이내면 충분함
> 워드프레스 100M일때 스케일아웃을 할때, 10 ->  100 확장될때, 100M어플리케이션을 구동하는데 1G이상의 OS영역이 필요함
>




Cahpter 2. INSTALLING DOCKER
==========================================
docs.docker.com
hub.docker.com

container
	chroot : runc
	cgroup : resource limit		
	namespace : isolate
		uts
		network
		mount
		pid
		user
		ipc
ubuntu
Install Docker Engine - Community 
1) Install using the repository
$ sudo apt-get update
$ sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common

Add Docker’s official GPG key AND URL
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
$ sudo add-apt-repository  "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs)    stable"

$ sudo apt-get update
$ sudo apt-get install docker-ce docker-ce-cli containerd.io


CentOS
Install Docker Engine - Community 
1) Install using the repository
yum install -y yum-utils device-mapper-persistent-data  lvm2
yum-config-manager   --add-repo     https://download.docker.com/linux/centos/docker-ce.repo

yum install docker-ce docker-ce-cli containerd.io -y
systemctl start docker
systemctl enable docker


2) Install from a package

3) Install using the convenience script





2. Kernel update
yum -y update
yum -y install yum-plugin-fastestmirror
rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
rpm -Uvh http://www.elrepo.org/elrepo-release-7.0-2.el7.elrepo.noarch.rpm
yum repolist

yum --enablerepo=elrepo-kernel install kernel-ml -y

grub2-set-default 0

cat << EOF > /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
net.ipv4.ip_forward = 1
EOF

sysctl --system

reboot
uname -a


- docker configuration file
# vim /etc/docker/daemon.json
{
  "insecure-registries": ["10.100.0.0/24"]
}

3. docker commands

$ docker run ubuntu echo hello
