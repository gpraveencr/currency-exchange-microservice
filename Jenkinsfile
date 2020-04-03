
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
		stage('package') {
			steps {
				sh 'mvn package -DskipTests'
			}
		}
		stage('Build Docker Image') {
			steps {

				//"docker build -t tennine/curreny-exchange-jenkins:$env.BUILD_TAG"
				script {
					dockerImage = docker.build("tennine/curreny-exchange-jenkins:$env.BUILD_TAG");
				}
			}
		}
		stage('Push Docker Image') {
			steps {
				script {
					docker.withRegistry('','dockerhub') {
						dockerImage.push();
						dockerImage.push('latest');
					}
				}
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