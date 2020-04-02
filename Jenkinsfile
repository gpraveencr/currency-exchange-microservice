
pipeline {
	agent any
	stages {
		stage('Build') {
			echo 'I\'m in Build stage'
		}
		stage('Deploy-to-Dev') {
			echo 'I\'m Deploying artifact to Dev servers'
		}
	}

	post {
		always {
			echo 'Script initiated'		
		}
		success {
			echo 'Yeah!! evrything ran well'
		}
		failure {
			echo 'Job didn\'t ran well'
		}
	}
}