pipeline {
	agent any
	tools {
		maven 'MonMaven'
	}
	stages {
		stage('Build') {
			steps {
				bat 'mvn clean package'
			}
			post {
				success {
					echo "Now archiving..."
					archiveArtifacts artifacts: '**/*.war'
				}
			}
		}
		stage('Deploy to Staging') {
			steps {
				build job: 'deploy-to-staging'
			}
		}
		stage('Deploy to Production') {
			steps {
				timeout(time: 5, unit: 'DAYS') {
					input message: 'Approve PRODUCTION deployment ?'
				}
				build job: 'deploy-to-prod'
			}
			post {
				success {
					echo "Code deplyed to PRODUCTION"
				}
				failure {
					echo "Deployment failed."
				}
			}
		}
	}
}