# Minikube Installation On AWS EC2


## What you’ll need
2 CPUs or more
2GB of free memory
20GB of free disk space
Internet connection
Container or virtual machine manager, such as: Docker, QEMU, Hyperkit, Hyper-V, KVM, Parallels, Podman, VirtualBox, or VMware Fusion/Workstation

### Step 1: We will create AWS EC2 t2.medium server Ubuntu server

### Step 2: Docker Instllation on Ubuntu
for this example I am considering the Docker as virtual machine manager.
So we will install docker first on the EC2 machine.

```sh
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y

```

### Step3: Add ubuntu user to docker group 

```sh
sudo usermod -aG docker ubuntu
```

### Step4: To install the latest minikube stable release on x86-64 Linux using binary download:


```sh
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube && rm minikube-linux-amd64
```
### Step 5: Start your cluster
```sh
minikube start
```
### Step 6: Install kubectl

```sh
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```
Test to ensure the version you installed is up-to-date:
kubectl version --client

### Step 7: Interact with your cluster
```sh
kubectl run demo-1 --image nginx
kubectl get pods
```
