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
		}
		stage ('Deploy') {
		}
	}
}
