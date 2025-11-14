pipeline {
	agent any

	tools {
		jdk 'Java-17'
		gradle 'Gradle-7.4'
	}

	stages {
		stage('Cloner le repo') {
			steps {
				git branch: 'main', url: 'https://github.com/00hiba00/Projet_Global_Devops.git'
			}
		}

		stage('Compiler') {
			steps {
				bat './gradlew clean build -x test -x spotlessJava -x spotlessCheck'
			}
		}

		stage('Tests unitaires') {
			steps {
				bat './gradlew test'
			}
			post {
				always {
					junit '*/build/test-results/test/.xml'
				}
			}
		}

		stage('Générer le package') {
			steps {
				bat './gradlew bootJar -x test -x spotlessJava -x spotlessCheck'
			}
		}

	}

	post {
		always {
			echo 'Pipeline terminé.'
		}
	}
}