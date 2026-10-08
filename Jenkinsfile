pipeline {
    agent any

    stages {

        stage('Test Environment') {
            steps {
                bat 'echo PATH=%PATH%'
                bat 'where cmd'
                bat 'where docker'
                bat 'docker --version'
            }
        }

    }
}