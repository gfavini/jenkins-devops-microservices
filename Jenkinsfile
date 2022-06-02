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
		stage('Build') {
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

		stage('Test') {
			steps {
				echo "Test"
			}
		}
		stage('Integraton Test') {
			steps {
				echo "Integraton Test"
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
