





after install openshift and before add metrics nedd install addition package 


```bash
yum install -y java-1.8.0-openjdk-headless
```

```bash

# ini new node for openshift cluster

# disk for docker volume 
export DISK=/dev/sde

yum install wget git net-tools bind-utils yum-utils iptables-services bridge-utils bash-completion kexec-tools sos psacct -y

yum -y install \
    https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm

sed -i -e "s/^enabled=1/enabled=0/" /etc/yum.repos.d/epel.repo

yum -y --enablerepo=epel install ansible pyOpenSSL

yum install docker-1.13.1 -y

cat <<EOF > /etc/sysconfig/docker-storage-setup
DEVS=${DISK}
VG=docker-vg
EOF

docker-storage-setup

systemctl enable docker

systemctl start docker
```
next run 
ansible-playbook -i enventory  playbooks/prerequisites.yml && \
 ansible-playbook -i enventory  playbooks/deploy_cluster.yml
