pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "ajithraj2525/exp10"
        DOCKER_TAG = "Devops"
    }

    stages {

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}:${DOCKER_TAG}")
                }
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-creds',
                        usernameVariable: 'USERNAME',
                        passwordVariable: 'PASSWORD'
                    )
                ]) {
                    bat 'echo %PASSWORD% | docker login -u %USERNAME% --password-stdin'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry(
                        'https://index.docker.io/v1/',
                        'dockerhub-creds'
                    ) {
                        docker.image("${DOCKER_IMAGE}:${DOCKER_TAG}").push()
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Image successfully built and pushed to Docker Hub'
        }

        failure {
            echo 'Pipeline failed'
        }
    }
}