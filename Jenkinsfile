pipeline {
    agent any

    stages {
        stage('Clone Code') {
            steps {
                echo 'Cloning the code'
                git url:"https://github.com/ShendeShubham17/LondheShubham153-django-notes-app.git", branch: "main"
            }
        }

        stage('Build') {
            steps {
                echo 'Building the image'
                sh "docker build -t my-note-app ."
            }
        }

        stage('Push to Dockerhub') {
            steps {
                echo 'Pushing the image to docker hub'
                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'DOCKERHUB_PASSWORD', usernameVariable: 'DOCKERHUB_USERNAME')]) {
                sh "docker tag my-note-app ${env.DOCKERHUB_USERNAME}/my-note-app:latest"
                sh 'docker login -u ${DOCKERHUB_USERNAME} -p ${DOCKERHUB_PASSWORD}'
                sh "docker push ${env.DOCKERHUB_USERNAME}/my-note-app:latest"
        
                }
                
            }
        }

        stage("Deploy"){
            steps {
                echo "Deploying the container"
                sh "docker-compose down && docker-compose up -d"
                
            }
        }
    }
}
