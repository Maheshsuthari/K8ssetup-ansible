This project contains a Vagrantfile and associated Ansible playbook scripts to provisioning a 3 nodes Kubernetes cluster using VirtualBox and Ubuntu 16.04.

Prerequisites
You need the following installed to use this playground.

Vagrant, version 1.9.3 or better. Earlier versions of vagrant do not work with the Vagrant Ubuntu 16.04 box and network configuration.
VirtualBox, tested with Version 5.1.18 r114002
Internet access, this playground pulls Vagrant boxes from the Internet as well as installs Ubuntu application packages from the Internet.
Bringing Up The cluster
To bring up the cluster, clone this repository to a working directory.

git clone http://github.com/davidkbainbridge/k8s-playground
Change into the working directory and vagrant up

cd k8ssetup-ansible
vagrant up
Vagrant will start three machines. Each machine will have a NAT-ed network interface, through which it can access the Internet, and a private-network interface in the subnet 172.42.42.0/24. The private network is used for intra-cluster communication.

The machines created are:

NAME	IP ADDRESS	ROLE
k8s1	172.42.42.1	Cluster Master
k8s2	172.42.42.2	Cluster Worker
k8s3	172.42.42.3	Cluster Worker
As the cluster brought up the cluster master (k8s1) will perform a kubeadm init and the cluster workers will perform a kubeadmin join. This cluster is using a static Kubernetes cluster token.

After the vagrant up is complete, the following command and output should be visible on the cluster master (k8s1).

vagrant ssh k8s1
kubectl -n kube-system get po -o wide```
