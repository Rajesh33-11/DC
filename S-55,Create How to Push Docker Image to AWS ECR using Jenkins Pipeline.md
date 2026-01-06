<img width="1842" height="206" alt="image" src="https://github.com/user-attachments/assets/0c77bab3-a3a7-45ce-9555-a7d844ffb855" /># How to Push Docker Image to AWS ECR using Jenkins Pipeline

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
<img width="1205" height="582" alt="image" src="https://github.com/user-attachments/assets/50f1a55b-4a7e-45a5-9136-c3c2878a4119" />

```
sh jenkins.sh
```
<img width="1917" height="962" alt="image" src="https://github.com/user-attachments/assets/ea4f2302-1d7b-4017-8e7b-453f64d9cde7" />


```
cat /var/lib/jenkins/secrets/initialAdminPassword
```
<img width="890" height="137" alt="image" src="https://github.com/user-attachments/assets/fe240cf5-4d25-4ce7-ba12-0d9cc49029e6" />

Install StageView Plugin
<img width="1882" height="572" alt="image" src="https://github.com/user-attachments/assets/e935902a-9578-4315-bbc4-d649f76de0e8" />
### Create a pipeline to get the code from Github to the server
<img width="1908" height="971" alt="image" src="https://github.com/user-attachments/assets/d3b61d01-cf0c-4bfb-b4e8-2f4f6ae41010" />


### save and Build pipeline
<img width="1918" height="920" alt="image" src="https://github.com/user-attachments/assets/99302680-f567-4852-99e9-814def11665d" />

### Verify in Server
```
cd /var/lib/jenkins/workspace/raja
```
```
ls
```
<img width="1842" height="206" alt="image" src="https://github.com/user-attachments/assets/47a676eb-297a-4e9c-95ae-e0399dd0089b" />



### install Docker
```
apt install docker.io -y
```
<img width="1647" height="555" alt="image" src="https://github.com/user-attachments/assets/710379ed-743f-4c4a-a97f-868d10288e05" />

----------------------

### Build image using Pipeline
```
pipeline {
    agent any
    stages {
        stage("gitCheckOut") {
            steps {
                git "https://github.com/azuredevops7/pwj-netflix-clone.git"
            }
        }
       stage("Build") {
            steps {
                sh "docker build -t test ."
            }
        }

    }
}

```
<img width="1918" height="977" alt="image" src="https://github.com/user-attachments/assets/c36bf475-674f-4138-8aec-2374db0f9605" />


----------------------

### Give Permission
```
chmod 777 /var/run/docker.sock
```
<img width="991" height="141" alt="image" src="https://github.com/user-attachments/assets/de546c9d-0c6d-49bd-a876-8862a4228f6d" />

----------------------
### Now Build and Verify in Server
<img width="1917" height="961" alt="image" src="https://github.com/user-attachments/assets/8032c6f2-187f-4eb0-812e-0800cebe0627" />
<img width="940" height="212" alt="image" src="https://github.com/user-attachments/assets/1999af1d-facb-48d2-bc5b-80db1e2c7203" />

