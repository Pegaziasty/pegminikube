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
sudo apt-get install --no-install-recommends qemu-system libvirt-clients libvirt-daemon-system

MiniKube:
wget https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo cp minikube-linux-amd64 /usr/local/bin/minikube
sudo chmod 755 /usr/local/bin/minikube

pegaz@peg01:~$ minikube version
minikube version: v1.23.2
commit: 0a0ad764652082477c00d51d2475284b5d39ceed

Kubectl:
curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl

chmod +x ./kubectl && sudo mv ./kubectl /usr/local/bin/kubectl

pegaz@peg01:~$ kubectl version -o json
{
  "clientVersion": {
    "major": "1",
    "minor": "22",
    "gitVersion": "v1.22.3",
    "gitCommit": "c92036820499fedefec0f847e2054d824aea6cd1",
    "gitTreeState": "clean",
    "buildDate": "2021-10-27T18:41:28Z",
    "goVersion": "go1.16.9",
    "compiler": "gc",
    "platform": "linux/amd64"
  }
}


Start Minikube:
minikube start










