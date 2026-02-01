pipeline {
	agent any
	environment {
		DOCKERHUB_CRED=credentials('dockerhub')
		IMAGE_NAME="gowri032/my-web-app"
	}
	
	stages {
		stage('checkout') {
			steps {
				git url:'https://github.com/Gowri0126/my-web-app', branch:'main' 
			}
		}
		
		stage('Build Docker Image') {
			steps {
				script {
					dockerImage=docker.build("my-web-app:latest")
				}
			}
		}
		
		stage('Push to DockerHub') {
			steps {
				script {
					docker.withRegistry('https://index.docker.io/v1/','dockerhub') {
						dockerImage.push()
					}
				}
			}
		}
	}
	
	post {
    always {
        echo 'Cleaning Up Workspace'
        node {
            deleteDir()
        }
    }
    failure {
        echo 'Pipeline Failed'
    }
}
}

