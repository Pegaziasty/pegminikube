# pegminikube
Minikube on Ubuntu 20.04.

Introduction

Minikube is an open source tool that allows you to set up a single-node Kubernetes cluster on your local machine. The cluster is run inside a virtual machine and includes Docker, allowing you to run containers inside the node.

To install Minikube on Ubuntu, follow the steps outlined below:

I use KVM and node: 
192.168.122.95 k8s-cluster.peg (2 CPUs, 2048 RAM as minimal)

Update && Upgrade:
sudo apt-get update -y && sudo apt-get upgrade -y && sudo apt autoremove && reboot

Install packages:
sudo apt-get install curl apt-transport-https -y

MiniKube:
wget https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo cp minikube-linux-amd64 /usr/local/bin/minikube
sudo chmod 755 /usr/local/bin/minikube








