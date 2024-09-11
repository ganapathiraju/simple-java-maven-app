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
				sh 'mvn -P metrics pmd:pmd
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
}
