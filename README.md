# Simple Notes App
### ✔️ Jenkins Declarative CI/CD Pipeline for DevOps Engineers 
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

## Docker compose
```sh
apt install docker-compose
```
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
____________________________________________________________________
### Install java first before download jenkins 
```sh
sudo apt-get update
  sudo apt-get install fontconfig openjdk-17-jre
  sudo apt-get install jenkins
```

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
______________________________________________________________________
- step -1
`Create AWS account`
- step 2
`Create EC2 instance`
- step 3
`Select - Amazon Machine Image (AMI) - UBUNTU
Create new key pair - login for SSH local terminal`
- step 4
`git clone Github-project-link
cd - Enter you project directory
sudo apt-get update`
- step 5
`sudo apt-get docker.io
docker --version
give permission to not use "sudo docker" - sudo usermod -aG docker $USER
sudo reboot`
- step 6
`Again access with SSH key
docker build -t notes-app .`
- step 7
`install java
sudo apt update
sudo apt install
openjdk-17-jre`
- step 8
`install jenkins
follow the link - https://pkg.jenkins.io/debian-stable/
`
```sh
service jenkins status
sudo usermod -aG docker jenkins
sudo systemctl restart jenkins
groups jenkins
```
- step 9
`open jenkins on browser copy public-ip from EC2 like http://3.110.207.109:8080/ jenkins port is 8080
EC2 instance in security gruop allow 8080 on your ip
Now user password and start jenkins`
- step 10
`After open jenkins select new-item and select pipelines
Enter an item name "choose yours" - notes-app-cicd`
- step 11
`select - GitHub project add links of git project
in "Advanced" write "Display name"`
- step 12
`Declarative pipeline write scrip in groovy language
This is script`
`If you want to push image on docker hub make jenkins system global credentials
docker hub username and password contein`
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
                sh "docker run -d -p 8000:8000 hackbugs/my-notes-app:latest" /*"docker-compose down && docker-compose up -d"*/
            }
        }
    }
}
```
- step 13
```sh
"docker login" on your EC2 terminal
Username - of DockerHub
Password - of DockerHub
```
- step 14
` install docker compose`
`cmd - sudo apt-get install docker-compose`
`docker-compose up -d`
`docker-compose down`
- step 15
` Also can direct groovy script can write in jinkins project in configruation`
`create groovy script in you git roject - and select in jenkins configruation - Pipeline script from SCM use groovy file name and location`
- step 16
` Everytime after changing in code not need to click in jenkins on "Build Now"`
` webhook steup inside github setting`
` github option "payload URL" paste your jenkins usr like ip port which you using to access of jenkins`
` like this - http://3.110.207.109:8080/github-webhook`

### Jenkins-CICD-django-notes-app - Configuration
- Pipeline
    - Pipeline script - in this we write groovy code
    - Pipeline script from SCM - in this groovy upload on github and set the path
______________________________________________________________________________________________________________
# ☑️CICD Pipeline Jenkins without java we can't run jenkins before installing jenkins first install java
### Version Control Github
- https://youtu.be/vxSXqvQy95g?si=GhH9MriOhJiNupRu

**Setups-Download-git,Downlaod-Java,Download-Apache-Maven,Downlaod-Jenkins**

## continus intgration mean
`continus Build + continus teat`

- CICD Mean you are writing code on your vscode and pushing on git and you can see on your sever means your web-application something has been changed
in between this things possible to happed due to jenkind

### Here's how you can describe the pipeline shown in the image:

1. **Developer (Code - Commit)**
   - The developer writes the code and commits it to a version control system (Git).

2. **Git**
   - The committed code is pushed to a remote repository hosted on Git.

3. **Jenkins**
   - Jenkins detects the new commit and triggers the CI/CD pipeline.

4. **Pipeline Stages:**
   - **Commit**
     - The pipeline is triggered by the code commit.
   
   - **Build**
     - Jenkins builds the application using tools like Maven, Gradle, or other build tools.

   - **Test**
     - The application undergoes automated testing (unit tests, integration tests, etc.).

   - **Stage**
     - The application is staged for deployment, preparing it for production. This may include further testing in a staging environment.

   - **Deploy**
     - The application is deployed to the production environment.

5. **Production**
   - The application is live and accessible to users.

### Jenkins Pipeline Script (Jenkinsfile)

```groovy
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                sh 'mvn clean install'  // Replace with your build command
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
                sh 'mvn test'  // Replace with your test command
            }
        }
        stage('Stage') {
            steps {
                echo 'Staging...'
                // Add your staging steps here
                // For example, deploying to a staging environment
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
                // Add your deploy steps here
                // For example, deploying to production
            }
        }
    }
}
```

- This script represents the pipeline shown in the image, with stages for build, test, stage, and deploy, running within Jenkins as part of a CI/CD process.

### jenkins port-number 8080
- jenkins is a framework and jenkins architecture is master-slave one master distribute task with slaves

### Pipeline of work
- ➡️ Developer ➡️ Github ➡️ Jenkins ➡️ Mavan for Build ➡️ selenium for Test ➡️ checkstyle for QA ➡️ deployment and delivery - delivery mean after building and test we give the project of client and deployment means we build test and deployment 

### Maven Building process
- ➡️ Maven ➡️ compile ➡️ code-review ➡️ unit-testing ➡️ intigration-testing ➡️ Packaging - war, jar

## Jinkins installation Getting Started by Defult first time install plugin list
Sure, here is a list of Jenkins plugins that you mentioned, which can be installed by default to extend its functionality:

### Jenkins Default Plugins

1. **Folders** - Organize jobs into hierarchical folders.
2. **OWASP Markup Formatter** - Provides security markup formatter for Jenkins.
3. **Build Timeout** - Configures build timeouts.
4. **Credentials Binding** - Allows credentials to be bound to environment variables.
5. **Timestamper** - Adds timestamps to the Console Output.
6. **Workspace Cleanup** - Cleans up the workspace before or after a build.
7. **Ant** - Integrates Apache Ant.
8. **Gradle** - Integrates Gradle.
9. **Pipeline** - Supports building continuous delivery pipelines.
10. **GitHub Branch Source** - Adds GitHub Branch as a source for multi-branch Pipeline.
11. **Pipeline: GitHub** - Integrates GitHub with Jenkins Pipeline.
12. **Groovy Libraries** - Loads Groovy libraries for Jenkins Pipeline.
13. **Pipeline Graph View** - Visualizes Jenkins Pipeline jobs.
14. **Git** - Integrates Git with Jenkins.
15. **SSH Build Agents** - Adds SSH build agents for Jenkins.
16. **Matrix Authorization Strategy** - Provides matrix-based security authorization.
17. **PAM Authentication** - Integrates PAM (Pluggable Authentication Modules) for authentication.
18. **LDAP** - Integrates LDAP for authentication.
19. **Email Extension** - Provides extended email notification functionality.
20. **Mailer** - Sends email notifications.
21. **Dark Theme** - Adds a dark theme to Jenkins for a better visual experience.

### Installing Plugins in Jenkins

To install these plugins, follow these steps:

1. **Access Jenkins Plugin Manager:**
   - Open Jenkins.
   - Go to "Manage Jenkins" > "Manage Plugins".

2. **Install Plugins:**
   - Search for each plugin name listed above.
   - Check the box next to each plugin.
   - Click on "Install without restart" or "Download now and install after restart".

### Jenkins CLI Installation Script

Alternatively, you can use the Jenkins CLI to install these plugins. Below is a script to install all the listed plugins using the Jenkins CLI:

```bash
# Download Jenkins CLI
wget http://localhost:8080/jnlpJars/jenkins-cli.jar

# Define Jenkins URL and credentials
JENKINS_URL=http://localhost:8080
JENKINS_USER=your_username
JENKINS_PASSWORD=your_password

# Install plugins
java -jar jenkins-cli.jar -s $JENKINS_URL -auth $JENKINS_USER:$JENKINS_PASSWORD install-plugin \
  cloudbees-folder \
  antisamy-markup-formatter \
  build-timeout \
  credentials-binding \
  timestamper \
  ws-cleanup \
  ant \
  gradle \
  workflow-aggregator \
  github-branch-source \
  pipeline-github \
  pipeline-groovy-lib \
  pipeline-graph-analysis \
  git \
  ssh-slaves \
  matrix-auth \
  pam-auth \
  ldap \
  email-ext \
  mailer \
  dark-theme

# Restart Jenkins to apply changes
java -jar jenkins-cli.jar -s $JENKINS_URL -auth $JENKINS_USER:$JENKINS_PASSWORD safe-restart
```

Replace `your_username` and `your_password` with your Jenkins credentials. Run this script in your terminal to install the plugins and restart Jenkins.

- This list ensures you have a robust Jenkins setup with essential plugins for various functionalities, enhancing your CI/CD pipeline.
______________________________________________________________________________________________________________________________________

## Jenkins Practice
- Jenkins Plugin Install
   - Maven intigration
   - Green Balls
    
- Jenkins Global Tool Configuration - we can set like environment variables path in jenkins inside Global Tool Configuration

- Pull project form github - PS C:\> git clone https://github.com/HackBugs/time-tracker.git
- cd C:\> cd .\time-tracker\
- CMD Of Maven - mvn clean package

