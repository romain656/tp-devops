pipeline {
    agent any

    environment {
        SONAR_TOKEN = credentials('sqa_bc23f71f502e5743c0517eae120363850706e0cb')
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/romain656/tp-devops.git'
            }
        }

        stage('Build') {
            steps {
                echo "Étape de build (à personnaliser selon ton projet)"
            }
        }

        stage('Analyse SonarQube') {
            steps {
                withSonarQubeEnv('test-sonar') {
                    sh 'sonar-scanner -Dsonar.login=$SONAR_TOKEN'
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
