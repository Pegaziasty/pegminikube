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


Managing Kubernetes with Minikube

To see the kubectl configuration use the command:

kubectl config view


apiVersion: v1
clusters:
- cluster:
    certificate-authority: /home/pegaz/.minikube/ca.crt
    extensions:
    - extension:
        last-update: Sat, 30 Oct 2021 20:41:07 CEST
        provider: minikube.sigs.k8s.io
        version: v1.23.2
      name: cluster_info
    server: https://192.168.39.49:8443
  name: minikube
contexts:
- context:
    cluster: minikube
    extensions:
    - extension:
        last-update: Sat, 30 Oct 2021 20:41:07 CEST
        provider: minikube.sigs.k8s.io
        version: v1.23.2
      name: context_info
    namespace: default
    user: minikube
  name: minikube
current-context: minikube
kind: Config
preferences: {}
users:
- name: minikube
  user:
    client-certificate: /home/pegaz/.minikube/profiles/minikube/client.crt
    client-key: /home/pegaz/.minikube/profiles/minikube/client.key
    
    
pegaz@ubuntu:~/mkube$ kubectl cluster-info
Kubernetes control plane is running at https://192.168.39.49:8443
CoreDNS is running at https://192.168.39.49:8443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.


pegaz@ubuntu:~/mkube$ kubectl get nodes
NAME       STATUS   ROLES                  AGE   VERSION
minikube   Ready    control-plane,master   91m   v1.22.2


pegaz@ubuntu:~/mkube$ minikube ssh
                         _             _            
            _         _ ( )           ( )           
  ___ ___  (_)  ___  (_)| |/')  _   _ | |_      __  
/' _ ` _ `\| |/' _ `\| || , <  ( ) ( )| '_`\  /'__`\
| ( ) ( ) || || ( ) || || |\`\ | (_) || |_) )(  ___/
(_) (_) (_)(_)(_) (_)(_)(_) (_)`\___/'(_,__/'`\____)

$ whoami
docker
$ hostname
minikube
$ date
Sat Oct 30 20:14:03 UTC 2021
$ w
 20:14:05 up 15 min,  0 users,  load average: 0.97, 0.45, 0.29
USER     TTY        LOGIN@   IDLE   JCPU   PCPU WHAT
$ exit
logout


pegaz@ubuntu:~/mkube$ minikube status
minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured

pegaz@ubuntu:~/mkube$ minikube addons list
|-----------------------------|----------|--------------|-----------------------|
|         ADDON NAME          | PROFILE  |    STATUS    |      MAINTAINER       |
|-----------------------------|----------|--------------|-----------------------|
| ambassador                  | minikube | disabled     | unknown (third-party) |
| auto-pause                  | minikube | disabled     | google                |
| csi-hostpath-driver         | minikube | disabled     | kubernetes            |
| dashboard                   | minikube | disabled     | kubernetes            |
| default-storageclass        | minikube | enabled ✅   | kubernetes            |
| efk                         | minikube | disabled     | unknown (third-party) |
| freshpod                    | minikube | disabled     | google                |
| gcp-auth                    | minikube | disabled     | google                |
| gvisor                      | minikube | disabled     | google                |
| helm-tiller                 | minikube | disabled     | unknown (third-party) |
| ingress                     | minikube | disabled     | unknown (third-party) |
| ingress-dns                 | minikube | disabled     | unknown (third-party) |
| istio                       | minikube | disabled     | unknown (third-party) |
| istio-provisioner           | minikube | disabled     | unknown (third-party) |
| kubevirt                    | minikube | disabled     | unknown (third-party) |
| logviewer                   | minikube | disabled     | google                |
| metallb                     | minikube | disabled     | unknown (third-party) |
| metrics-server              | minikube | disabled     | kubernetes            |
| nvidia-driver-installer     | minikube | disabled     | google                |
| nvidia-gpu-device-plugin    | minikube | disabled     | unknown (third-party) |
| olm                         | minikube | disabled     | unknown (third-party) |
| pod-security-policy         | minikube | disabled     | unknown (third-party) |
| portainer                   | minikube | disabled     | portainer.io          |
| registry                    | minikube | disabled     | google                |
| registry-aliases            | minikube | disabled     | unknown (third-party) |
| registry-creds              | minikube | disabled     | unknown (third-party) |
| storage-provisioner         | minikube | enabled ✅   | kubernetes            |
| storage-provisioner-gluster | minikube | disabled     | unknown (third-party) |
| volumesnapshots             | minikube | disabled     | kubernetes            |
|-----------------------------|----------|--------------|-----------------------|

pegaz@ubuntu:~/mkube$ minikube dashboard
🔌  Enabling dashboard ...
    ▪ Using image kubernetesui/metrics-scraper:v1.0.7
    ▪ Using image kubernetesui/dashboard:v2.3.1
🤔  Verifying dashboard health ...
🚀  Launching proxy ...
🤔  Verifying proxy health ...
🎉  Opening http://127.0.0.1:33713/api/v1/namespaces/kubernetes-dashboard/services/http:kubernetes-dashboard:/proxy/ in your default browser...
^C

Or:

pegaz@ubuntu:~/mkube$ minikube dashboard --url
🤔  Verifying dashboard health ...
🚀  Launching proxy ...
🤔  Verifying proxy health ...
http://127.0.0.1:34601/api/v1/namespaces/kubernetes-dashboard/services/http:kubernetes-dashboard:/proxy/














