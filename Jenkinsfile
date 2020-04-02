
pipeline {
	//agent any
	agent { docker {image 'maven:3.6.3'}}
	stages {
		stage('Build') {
			steps {
				sh 'mvn --version'
				echo 'I\'m in Build stage'
			}
		}
		stage('Deploy-to-Dev') {
			steps {
				echo 'I\'m Deploying artifact to Dev servers'
			}
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