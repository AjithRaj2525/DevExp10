```groovy
pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "ajithraj2525/exp10"
        DOCKER_USERNAME = "ajithraj2525"
    }

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/AjithRaj2525/DevExp10.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %DOCKER_IMAGE%:t1 .'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([
                    string(
                        credentialsId: 'dockerhub-PAT',
                        variable: 'DOCKER_PAT'
                    )
                ]) {
                    bat '''
                        @echo off
                        echo %DOCKER_PAT% | docker login -u %ajithraj2525% --password-stdin
                    '''
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                bat 'docker push %DOCKER_IMAGE%:t1'
            }
        }
    }

    post {
        success {
            echo 'Docker image built and pushed successfully.'
        }

        failure {
            echo 'Pipeline failed. Check Console Output.'
        }
    }
}
```