pipeline{
	agent any
	environment{
		DOCKER_IMAGE = "ajithraj2525/exp10"
	}
	stages{
		stage('Clone Repository'){
			steps{
				git 'https://github.com/AjithRaj2525/DevExp10.git'
			}
		}
	stage('Build Docker Image'){
		steps{
			script{
				docker.build("${DOCKER_IMAGE}:latest")
			}
		}
	}
	stage('Login to Docker Hub'){
		steps{
			withCredentials([usernamePassword(
				credentialsId: 'dockerhub-creds',
				usernameVariable: 'DOCKER_USER',
				passwordVariable: 'DOCKER_PASS'
 			)] {
				bat 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
			}
		}											
	}
	stage('push Docker Image') {
		steps{
			script {
				docker.withRegistry('','dockerhub-creds'){
					docker.image("${DOCKER_IMAGE}:latest").push()
				}
			}
		}
	}
}	
post {
	success{
		echo 'Image successfully built and pushed to Docker Hub'
	}
	failure{
		echo 'Pipeline failed'
	}
}
}  
	


	