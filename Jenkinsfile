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
	// agent {docker {image 'maven:3.6.3'}}
	agent {docker {image 'node:13.8'}}
	stages{
		stage('Build') {
			steps {
				echo "Build"
				sh "node --version"
				
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
