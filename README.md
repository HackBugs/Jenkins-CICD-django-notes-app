# Simple Notes App
### Jenkins Declarative CI/CD Pipeline for DevOps Engineers 
This is a simple notes app built with React and Django.

## Requirements
1. Python 3.9
2. Node.js
3. React

## Installation
1. Clone the repository
```
git clone https://github.com/LondheShubham153/django-notes-app.git
```

2. Build the app
```
docker build -t notes-app .
```

3. Run the app
```
docker run -d -p 8000:8000 notes-app:latest
```

## Nginx

- Install Nginx reverse proxy to make this application available

`sudo apt-get update`
`sudo apt install nginx`

- add your user to the Docker group
```sh
sudo usermod -aG docker $USER
```
- Add Jenkins User to Docker Group:
```sh
sudo usermod -aG docker jenkins
sudo systemctl restart jenkins
groups jenkins
```
### if docker is not runnign in some case use this CMD
It looks like you mistyped the command. Instead of `dicker`, you should use `docker`. Here's the corrected command:

```bash
docker build -t notes-app .
```

Make sure you have Docker installed and running on your system. If you encounter any issues with Docker, you can check the Docker service status:

```bash
sudo systemctl status docker
```

If Docker is not installed, you can install it using:

```bash
sudo apt update
sudo apt install docker.io
```

Once installed, you can start the Docker service and enable it to start on boot:

```bash
sudo systemctl start docker
sudo systemctl enable docker
```

----------------------------------------------------------
### groovy code and script inside jenkins
```sh
pipeline {
    agent any
    stages {
        stage('cloning Code') {
            steps {
                echo 'Cloning the code'
                git url:'https://github.com/HackBugs/django-notes-app.git', branch: 'main'
            }
        }
        stage('Build') {
            steps {
                echo 'Building the code'
                sh 'docker build -t my-notes-app .'
            }
        }
        stage('Push to Docker Hub') {
            steps {
                echo 'Push the image to Docker Hub'
                withCredentials([usernamePassword(credentialsId:"dockerHub" ,passwordVariable:"dockerHubPass", usernameVariable:"dockerHubUser")]){
                sh "docker tag my-notes-app ${env.dockerHubUser}/my-notes-app:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/my-notes-app:latest"
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying the container'
                sh "docker-compose" /* "docker run -d -p 8000:8000 hackbugs/my-notes-app:latest" */
            }
        }
    }
}
```
-------------------------------------------------------------------------
### Jenkins insatll on ubuntu Debian Packages
- This is the Debian package repository of Jenkins to automate installation and upgrade. To use this repository, first add the key to your system (for the Weekly Release Line):
```sh
 sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
    https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
```
- Then add a Jenkins apt repository entry:
```sh
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
    https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
    /etc/apt/sources.list.d/jenkins.list > /dev/null
 ```
- Update your local package index, then finally install Jenkins:
```sh
sudo apt-get update
  sudo apt-get install fontconfig openjdk-17-jre
  sudo apt-get install jenkins
```
- The apt packages were signed using this key:
```sh
pub   rsa4096 2023-03-27 [SC] [expires: 2026-03-26]
      63667EE74BBA1F0A08A698725BA31D57EF5975CA
uid                      Jenkins Project 
sub   rsa4096 2023-03-27 [E] [expires: 2026-03-26]
```
-------------------------------------------------------------------
```sh
- step -1
Create AWS account 
- step 2
Create EC2 instance
- step 3
Select - Amazon Machine Image (AMI) - UBUNTU
Create new key pair - login for SSH local terminal
- step 4
git clone Github-project-link
cd - Enter you project directory
sudo apt-get update
- step 5
sudo apt-get docker.io
docker --version
give permission to not use "sudo docker" - sudo usermod -aG docker $USER
sudo reboot
- step 6
Again access with SSH key
docker build -t notes-app .
- step 7
install java
sudo apt update
sudo apt install
openjdk-17-jre
- step 8
install jenkins
follow the link - https://pkg.jenkins.io/debian-stable/
service jenkins status
- step 9
open jenkins on browser copy public-ip from EC2 like http://3.110.207.109:8080/ jenkins port is 8080
EC2 instance in security gruop allow 8080 on your ip
Now user password and start jenkins
- step 10
```
