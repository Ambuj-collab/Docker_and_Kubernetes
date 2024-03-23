# Minikube Installation

### Install Alma Linux VM
- Login to vSphere
- Create a VM > Deploy from template > Choose Base-Alma9-v3-ESXi6...
- The VM settings should be 2 CPUs, 8 GB memory and 50GB hard disk
- Install putty on your laptop
- SSH into the box using putty. Login with credentials alma/changeMe1234

### Update VM
https://idroot.us/install-minikube-almalinux-9/
```
sudo dnf clean all
sudo dnf update
sudo dnf install -y curl kubectl
```

### Create user 'voltage'
```
sudo useradd -m -s /bin/bash voltage
sudo passwd voltage
sudo usermod -aG wheel voltage
su - voltage
```

### Download ```kubectl```
```
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
sudo mv kubectl /usr/local/bin/
```

### Download minikube
```
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```

### Download and Run Docker Engine
https://docs.docker.com/engine/install/fedora/
```
sudo dnf -y install dnf-plugins-core
sudo dnf config-manager \
--add-repo=https://download.docker.com/linux/centos/docker-ce.repo
sudo dnf install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
sudo systemctl start docker
sudo docker run hello-world
```

### Start Minikube
```
minikube start --driver=docker
minikube config set driver docker
kubectl get pods -A
```


