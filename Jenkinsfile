// Scripted
// node {
// 	stage('Build') {
// 		echo "Build"
// 	}
// 	stage('Test') {
// 		echo "Test"
// 	}
// 	stage('Integraton Test') {
// 		echo "Integraton Test"
// 	}
// }

// Declarative
pipeline {
	agent any
	// agent {docker {image 'maven:3.6.3'}}
	// agent {docker {image 'node:13.8'}}
	environment {
		dockerHome = tool "my_docker"
		mavenHome = tool "my_maven"
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}

	stages{
		stage('Checkout') {
			steps {
				echo "Build"
				sh "mvn --version"
				sh "docker version"
				echo "Path - $PATH"
				echo "Build Number - $env.BUILD_NUMBER"
				echo "Build ID - $env.BUILD_ID"
				echo "Job - $env.JOB_NAME"
				echo "Build tag - $env.BUILD_TAG"
				echo "Build URL - $env.BUILD_URL"
			}
		}
		stage('Compile') {
			steps {
				sh "mvn clean compile"
			}
		}		
		stage('Test') {
			steps {
				sh "mvn test"
			}
		}
		stage('Integraton Test') {
			steps {
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}
		stage('Package') {
			steps {
				sh "mvn package -DskipTest"
			}
		}

		stage('Build Docker Image') {
			steps {
				script {
					dockerImage = docker.build("gfavini/currency-exchange-devops:${env.BUILD_TAG}");
				}
			}
		}
		stage('Push Docker Image') {
			steps {
				// "docker build -t gfavini/currency-exchange-devops:$env.BUILD_TAG"
				script {
					docker.withRegistry('', 'dockerhub'){
						dockerImage.push();
						dockerImage.push('latest')
					}
					
				}
			}
		}
	} 
	post {
		always{
			echo 'Eu sempre rodo'
		}
		success {
			echo 'Somente rodo quando tenho sucesso'
		}
		failure {
			echo 'eu so rodo em falha'
		}
	}

}
