pipeline {
	agent any
	tools {
		maven 'maven'
	}
	stages {
		stage ('Build') {
			steps {
				sh 'mvn -B -DskipTests clean package'
			}
		}
		stage ('CodeReview') {
			steps {
				gerritReview labels: [Verified: 0] 
				echo 'Hello World'
			}
			post {
				success {
					gerritReview labels: [Verified: 1]
					gerritCheck checks: ['example:checker': 'SUCCESSFUL']
				}
				unstable {
					gerritReview labels: [Verified: 0],
					message: 'Build is unstable'
				}
				failure {
					gerritReview labels: [Verified: -1]
					gerritCheck checks: ['example:checker': 'FAILED'],
					message: 'Invalid Syntax'
				}
			}
		}
		stage ('Test') {
			steps {
				sh 'mvn test'
			}
			post {
				always {
					junit 'target/surefire-reports/*.xml'
				}
			}
		}
		stage ('Package') {
			steps {
				sh 'mvn clean package'
			}
		}
	}
	post {
		success {
	}
}
