# Git → Maven → Jenkins → Docker → ECR → SonarQube → K8S Cluster
------------------------------------------------
## Rerequirements:
#### -CREATE EC2 USING UBUNTU WITH 30 GB EBS AND INSTANCE_TYPE BE M7I-FLUX.LARGE(Eg: 8 CPUS, 32GB RAM),
#### -CREATE IAM ROLE WITH ADMIN ACCESS ADD THE ROLE TO YOUR  EC2 SERVER
------------------------------------------------
# Setup Jenkins
```
vim jenkins.sh
```
```
sudo apt update -y
sudo apt upgrade -y
sudo apt install git openjdk-8-jdk maven -y
sudo apt install -y openjdk-17-jdk
java -version
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null

echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt update -y
sudo apt install -y jenkins
update-alternatives --config java
sudo systemctl start jenkins
sudo systemctl enable jenkins
sudo systemctl status jenkins
```
<img width="1107" height="545" alt="image" src="https://github.com/user-attachments/assets/63154375-4839-4237-b434-439ae904988d" />

```
sh jenkins.sh
```
------------------------------
# Install Docker

```
apt install docker.io -y
```
<img width="1565" height="519" alt="image" src="https://github.com/user-attachments/assets/a66f9c6b-cb7f-4c55-9581-af633e8b0d1d" />

------------------------------
# Setup a cluster
### Installing kubectl
```
# Download the latest kubectl binary
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

# Validate the binary (optional but recommended)
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check

# Install kubectl
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl

# Verify installation
kubectl version --client
```
<img width="1508" height="570" alt="image" src="https://github.com/user-attachments/assets/ac8bf054-2c2d-461d-9e82-7a3a606c99f4" />

### Installing kops
```
# Download the latest kops binary
curl -LO https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64

# Make it executable
chmod +x kops-linux-amd64

# Move to system path
sudo mv kops-linux-amd64 /usr/local/bin/kops

# Verify installation
kops version
```
<img width="1862" height="465" alt="image" src="https://github.com/user-attachments/assets/0e4eaac3-f207-4155-9785-8119dee24dbb" />

### Installing AWS CLI
```
apt update && apt install unzip -y

curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

------------------------------
# Setup a cluster
