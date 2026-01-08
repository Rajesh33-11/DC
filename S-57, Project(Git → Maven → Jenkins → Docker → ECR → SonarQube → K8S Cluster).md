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
<img width="925" height="187" alt="image" src="https://github.com/user-attachments/assets/a0165246-d423-443c-a899-40284fe96b02" />

------------------------------
# Create S3 bucket for kOps state store
```
aws s3 mb s3://55rajesh.k8s.locals
aws s3api put-bucket-versioning --bucket 55rajesh.k8s.locals --region ap-south-1 --versioning-configuration Status=Enabled
export KOPS_STATE_STORE=s3://55rajesh.k8s.locals
```
<img width="1486" height="201" alt="image" src="https://github.com/user-attachments/assets/a2e9aa0d-9582-4dd1-b936-be6f88109ef5" />

--------------------------------
# This command creates a Kubernetes cluster configuration using kOps on AWS
```
kops create cluster --name=rajesh33.k8s.local --zones=ap-northeast-3a --control-plane-size=m7i-flex.large --control-plane-count=1 --node-count=2 --node-size=t3.micro --image=ami-06571d6ae17e327ff
```
<img width="1867" height="537" alt="image" src="https://github.com/user-attachments/assets/c96af9e9-b7c2-45bf-b633-abed61ed36aa" />

# update cluster
```
kops update cluster --name rajesh33.k8s.local --yes --admin
```
--------------------------------
# I want create Sonarcube container
```
docker run -itd --name  con1 -p 9000:9000 sonarqube:8.7-community
```
<img width="1762" height="450" alt="image" src="https://github.com/user-attachments/assets/68879062-7e3c-4242-9c19-092f9618ee39" />

# Access Sonarcube container
```
Public_ip:9000
```
<img width="1908" height="998" alt="image" src="https://github.com/user-attachments/assets/2edc4416-2bd0-46a5-86c8-1d6d67500542" />
Defualt - User_name: admin, Password: admin
<img width="1918" height="967" alt="image" src="https://github.com/user-attachments/assets/b1eb5ab9-a29a-421f-9ab0-2b4aefc1844b" />

--------------------------------
# Create a pipeline Clone the website files from GitHub to the server.
```
pipeline {
    agent any

    stages {
        stage("Git Checkout") {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Rajesh33-11/char-webapp33.git'
            }
        }
    }
}

```
Now build and verify in Server for files
