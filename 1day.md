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

> MSA 추세로 시스템 하나에 어플리케이션 하나가 구축되는 추세임

> 워드프레스가 100M일때 스케일아웃되어 10 ->  100개씩 확장될때, 100M 어플리케이션을 구동하는데 1G이상의 OS영역이 필요하고, 함께 복제됨.

> 100M를 복제하는것와 1.5G를 복제하는것은 비용이 다름

> App 버전1 출시 -> 고객의 니즈 변화, 버튼 색변경 -> App 버전2 출시 필요

> 컨테이너는 OS위의 APP과 Bins'Libs(서비스 환경에 필요한 라이브러리)영역임

> Docker만 구동할 수 있으면, OS등 환경 영향을 안받고 서비스 가능함

> 가상환경보다 더 빠르게 배포할 수 있으므로, 고객 니즈에 빠르게 대응할 수 있으므로 수익 증가!!

> 각사의 환경에 맞춰 Docker 머신을 운용함
> >하이퍼바이져 위에 가상머신 두고 위에 Docker 구동
> >베어메탈 위에 Docker 구동
> 컨테이너의 운영 수가 증가함에 따라 오케스트레이션 도구의 필요성이 증가됨
> > 도커 스웜, 쿠버네티스 중요성 증가
> > > 리소스는 아껴쓰는게 아니라, 잘 써야됨!


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
