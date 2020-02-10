Cahpter 1. CONTAINER TECHNOLOGY OVERVIEW
==========================================

## 베어메탈 환경
리소스 효율성을 위해 한 서버위에 여러 어플리케이션을 올려서 사용함
 -
## 가상화 환경
H/W 가격 


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

Cahpter 2. INSTALLING DOCKER
==========================================
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
