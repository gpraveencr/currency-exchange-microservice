
pipeline {
	agent any
	//agent { docker {image 'maven:3.6.3'}}

	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$mavenHome/bin:$dockerHome/bin:$PATH"
	}
	stages {
		stage('Checkout') {
			steps {
				sh 'mvn --version'
				sh 'docker version'
				echo 'I\'m in Build stage'
			}
		}
		stage('Build') {
			steps {
				sh 'mvn clean compile'
			}
		}
		stage('Deploy-to-Dev') {
			steps {
				echo 'I\'m Deploying artifact to Dev servers'
				sh 'mvn test'
			}
		}
		stage('Integration Test') {
			steps {
				echo 'In Integration Tests'
				sh 'mvn failsafe:integration-test failsafe:verify'
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