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
	}
}