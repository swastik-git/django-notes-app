@Library('Shared')_
pipeline {
    agent { label 'agent_1' }

    stages {
        stage('Code clone') {
            steps {
                clean_ws()
                clone('https://github.com/swastik-git/django-notes-app.git', 'main')
            }
        }
        stage('Code Build') {
            steps {
                docker_build(imageName:'notes-app')
            }
        }
        stage('Push to DockerHub') {
            steps {
                docker_push(
                    imageName: 'notes-app',
                    imageTag: 'latest',
                    credentials: 'docker_hub_creds'
                )
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker run -d -p 8000 notes-app:latest'
                echo 'Deploying the application...'
            }
        }
    }
}
