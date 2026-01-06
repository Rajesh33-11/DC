<img width="1916" height="968" alt="image" src="https://github.com/user-attachments/assets/85589c4b-c155-4f53-98c7-67f658cdc8df" /># How to Push Docker Image to AWS ECR using Jenkins Pipeline

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
<img width="1151" height="517" alt="image" src="https://github.com/user-attachments/assets/a151b0c0-cce3-415c-a83e-d8fc7999c0ff" />

```
sh jenkins.sh
```
<img width="1913" height="967" alt="image" src="https://github.com/user-attachments/assets/e1493e00-335f-4827-81f3-bc0c7de851f7" />

```
cat /var/lib/jenkins/secrets/initialAdminPassword
```
<img width="917" height="162" alt="image" src="https://github.com/user-attachments/assets/9da12a7b-fbb6-4a46-8565-41c7d7e9332f" />
Install StageView Plugin
<img width="1882" height="572" alt="image" src="https://github.com/user-attachments/assets/e935902a-9578-4315-bbc4-d649f76de0e8" />
### Create a pipeline to get the code from Github to the server
<img width="1886" height="955" alt="image" src="https://github.com/user-attachments/assets/4d3adcc6-ed35-49c9-9293-bb2f555765aa" />

### save and Build pipeline
<img width="1912" height="938" alt="image" src="https://github.com/user-attachments/assets/eac17b5b-d4a2-438e-9f9b-8b4c01b9f876" />

### Verify in Server
```
cd /var/lib/jenkins/workspace/raja
```
```
ls
```
<img width="1010" height="250" alt="image" src="https://github.com/user-attachments/assets/b09752e6-856b-40fb-a949-fa3860bbbf89" />

### install Docker
```
apt install docker.io -y
```
<img width="1647" height="555" alt="image" src="https://github.com/user-attachments/assets/710379ed-743f-4c4a-a97f-868d10288e05" />



