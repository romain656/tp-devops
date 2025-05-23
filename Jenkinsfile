pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo "Étape de build (à personnaliser selon ton projet)"
            }
        }

        stage('Analyse SonarQube') {
            steps {
                withCredentials([string(credentialsId: 'sonarqube-token', variable: 'SONAR_TOKEN')]) {
                    withSonarQubeEnv('SonarQubeServer') {
                        sh 'sonar-scanner -Dsonar.login=$SONAR_TOKEN'
                    }
                }
            }
        }

        stage('Déploiement') {
            steps {
                echo "Étape de déploiement"
            }
        }
    }
}
