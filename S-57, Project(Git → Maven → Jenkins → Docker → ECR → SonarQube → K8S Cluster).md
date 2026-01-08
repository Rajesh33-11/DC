# Git → Maven → Jenkins → Docker → ECR → SonarQube → K8S Cluster
------------------------------------------------
## Rerequirements:
#### -CREATE EC2 USING UBUNTU WITH 30 GB EBS AND INSTANCE_TYPE BE M7I-FLUX.LARGE(Eg: 8 CPUS, 32GB RAM),
#### -CREATE IAM ROLE WITH ADMIN ACCESS ADD THE ROLE TO YOUR  EC2 SERVER
------------------------------------------------
### Setup Jenkins
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
