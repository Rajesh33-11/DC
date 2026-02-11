# Create Cluster EKS and Deploy
------------------------------------------------
## Rerequirements:
#### -CREATE EC2 USING UBUNTU WITH 30 GB EBS AND INSTANCE_TYPE BE T2.XLARGE(Eg: 4 CPUS, 32GB RAM),
#### -CREATE IAM ROLE WITH ADMIN ACCESS ADD THE ROLE TO YOUR  EC2 SERVER
------------------------------------------------
### create a ubuntu Server install Jenkins
```
vim jenkins.sh
```
```
sudo apt update -y
sudo apt upgrade -y
sudo apt install git openjdk-8-jdk maven -y
sudo apt install -y openjdk-17-jdk
java -version
sudo rm -f /etc/apt/sources.list.d/jenkins.list
sudo rm -f /usr/share/keyrings/jenkins-keyring.*
sudo apt update
sudo apt install fontconfig openjdk-21-jre -y  # Install Java first[page:1]
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc https://pkg.jenkins.io/debian-stable/jenkins.io-2026.key
echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/" | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt update
sudo apt install jenkins -y
update-alternatives --config java
sudo systemctl start jenkins
sudo systemctl enable jenkins
sudo systemctl status jenkins
```
<img width="1885" height="566" alt="image" src="https://github.com/user-attachments/assets/526a1bee-a39c-4211-b18b-af9a07061300" />


```
sh jenkins.sh
```
### Installing AWS CLI
```
apt update && apt install unzip -y

curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
aws configure
```
<img width="982" height="216" alt="image" src="https://github.com/user-attachments/assets/b6616f96-c2a2-42b0-b057-ce33ff3d6bb8" />

_________________________________________________

# Install Kubectl 
## 1️⃣ Download the latest stable kubectl binary
```
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```
- Explanation:
- curl → Downloads data from a URL
-L → Follows redirects
-O → Saves the file with the same name as in the URL (kubectl)
Inner curl:
Reads the latest stable Kubernetes version from stable.txt
Example output: v1.30.x
linux/amd64/kubectl → Downloads kubectl for Linux 64-bit

### 📌 Result:
Latest stable kubectl binary is downloaded to the current directory.

## 2️⃣ Give execute permission
```
chmod +x kubectl
```
Explanation:
Adds execute permission to the kubectl binary
Required to run it as a command
## 📌 Without this, Linux will block execution.

## 3️⃣ Move kubectl to system PATH
```
mv kubectl /usr/local/bin/kubectl
```
Explanation:
Moves kubectl to /usr/local/bin
This directory is already part of the system $PATH
## 📌 Benefit:
You can run kubectl from any directory.
⚠️ In most systems this should be:
sudo mv kubectl /usr/local/bin/
## 4️⃣ Verify kubectl installation
```
kubectl version
```
Explanation:
Confirms kubectl is installed
Shows client and server version (server appears only if a cluster is connected)
## 📌 Recommended check:
kubectl version --client
__________________________________________________________________________________________________________________________________

# Install Eksctl
### Installing eksctl – Step-by-Step Explanation

## 🔹 What is eksctl?
      eksctl is a CLI tool used to:
       - Create EKS clusters
       -  Create node groups
       -  Delete clusters
       -  Manage EKS easily from terminal

### In real-time companies, most EKS clusters are created using eksctl + CLI, not manually from console.

### Download eksctl
```
sudo wget https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz
```
### What this does:

**wget → Downloads file from internet**

**$(uname -s) → Detects your OS automatically (Linux/Darwin)**

**amd64 → 64-bit architecture**

**Downloads compressed file (.tar.gz)**

👉 This downloads the latest eksctl version.

### 2️⃣ Extract & Move to System Path
```
sudo tar -xzvf eksctl_$(uname -s)_amd64.tar.gz -C /usr/local/bin
```
Breakdown:

tar → Extract archive

-x → extract

-z → unzip gzip

-v → verbose

-f → file

-C /usr/local/bin → extract directly into system bin folder

## 👉 Why /usr/local/bin?

Because it is in system PATH.

So you can run:
```
eksctl
```
from anywhere in terminal.

### 3️⃣ Verify Installation
```
eksctl version
```
