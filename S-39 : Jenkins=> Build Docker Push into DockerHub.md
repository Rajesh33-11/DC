
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
