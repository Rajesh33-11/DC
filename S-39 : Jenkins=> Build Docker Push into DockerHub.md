
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
<img width="1893" height="562" alt="image" src="https://github.com/user-attachments/assets/b06ab2f5-fe95-4c00-b2bd-dd823bda34c7" />


```
sh jenkins.sh
```
------------------------------
# Install Docker

```
apt install docker.io -y
```
<img width="1165" height="297" alt="image" src="https://github.com/user-attachments/assets/706431d7-c5a2-49d3-a024-375d77693499" />

------------------------------
<img width="1917" height="803" alt="image" src="https://github.com/user-attachments/assets/bba68fbf-27fb-485b-b5ff-224bee41cebf" />

------------------------------
<img width="1918" height="991" alt="image" src="https://github.com/user-attachments/assets/c65a06e6-fadb-4239-8884-aa94749a2396" />

------------------------------
<img width="1354" height="410" alt="image" src="https://github.com/user-attachments/assets/7eb0d0d0-a6b0-4247-b3f0-435402f2fd1a" />
<img width="1910" height="538" alt="image" src="https://github.com/user-attachments/assets/e10fdd81-d6f8-4a92-94b8-9f513299062b" />

--------------------------
```
pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/vijay2181/springboot-mongo-docker.git'
            }
        }
    }
}
```
<img width="1727" height="811" alt="image" src="https://github.com/user-attachments/assets/4afd6540-7019-44a9-8be6-ad37fcb6d4ce" />

---
<img width="1402" height="296" alt="image" src="https://github.com/user-attachments/assets/82fb9846-a53c-46af-a62f-dbe8a21f2ae4" />

```
chmod  777 /var/run/docker.sock
```
```
pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/vijay2181/springboot-mongo-docker.git'
            }
        }
        stage("Build") {
            steps {
                sh "docker build -t carrer ."
            }
            }
        }
    }
}
```



