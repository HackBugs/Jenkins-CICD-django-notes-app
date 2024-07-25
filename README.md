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

Install Nginx reverse proxy to make this application available

`sudo apt-get update`
`sudo apt install nginx`

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
