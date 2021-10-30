# pegminikube
Minikube on Ubuntu 20.04.

Introduction

Minikube is an open source tool that allows you to set up a single-node Kubernetes cluster on your local machine.
The cluster is run inside a virtual machine and includes Docker, allowing you to run containers inside the node.

To install Minikube on Ubuntu, follow the steps outlined below:

Update && Upgrade:

sudo apt-get update -y && sudo apt-get upgrade -y && sudo apt autoremove && reboot

Install packages:

sudo apt-get install curl apt-transport-https -y

sudo apt-get install --no-install-recommends qemu-system libvirt-clients libvirt-daemon-system && reboot

MiniKube:

mkdir mkube && cd mkube

wget https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64

sudo cp minikube-linux-amd64 /usr/local/bin/minikube && sudo chmod 755 /usr/local/bin/minikube


pegaz@ubuntu:~/mkube$ minikube version

minikube version: v1.23.2

commit: 0a0ad764652082477c00d51d2475284b5d39ceed


Kubectl:

curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl

chmod +x ./kubectl && sudo mv ./kubectl /usr/local/bin/kubectl

pegaz@ubuntu:~/mkube$ kubectl version -o json

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

pegaz@ubuntu:~/mkube$ minikube start
😄  minikube v1.23.2 on Ubuntu 20.04
✨  Automatically selected the kvm2 driver
💾  Downloading driver docker-machine-driver-kvm2:
    > docker-machine-driver-kvm2....: 65 B / 65 B [----------] 100.00% ? p/s 0s
    > docker-machine-driver-kvm2: 11.40 MiB / 11.40 MiB  100.00% 25.62 MiB p/s 
💿  Downloading VM boot image ...
    > minikube-v1.23.1.iso.sha256: 65 B / 65 B [-------------] 100.00% ? p/s 0s
    > minikube-v1.23.1.iso: 225.22 MiB / 225.22 MiB  100.00% 25.57 MiB p/s 9.0s
👍  Starting control plane node minikube in cluster minikube
💾  Downloading Kubernetes v1.22.2 preload ...
    > preloaded-images-k8s-v13-v1...: 511.69 MiB / 511.69 MiB  100.00% 25.77 Mi
🔥  Creating kvm2 VM (CPUs=2, Memory=2200MB, Disk=20000MB) ...
❗  This VM is having trouble accessing https://k8s.gcr.io
💡  To pull new external images, you may need to configure a proxy: https://minikube.sigs.k8s.io/docs/reference/networking/proxy/
🐳  Preparing Kubernetes v1.22.2 on Docker 20.10.8 ...
    ▪ Generating certificates and keys ...
    ▪ Booting up control plane ...
    ▪ Configuring RBAC rules ...
🔎  Verifying Kubernetes components...
    ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5
🌟  Enabled addons: storage-provisioner, default-storageclass
🏄  Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default













