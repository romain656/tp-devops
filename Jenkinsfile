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

        stage('Update values.yaml') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'github-push-token', usernameVariable: 'GIT_USERNAME', passwordVariable: 'GIT_TOKEN')]) {
                    script {
                        def newTag = "v${BUILD_NUMBER}"
                        sh "sed -i 's|romain656/tp-devops:.*|romain656/tp-devops:${newTag}|' values.yaml"
                        sh "git config user.email 'jenkins@example.com'"
                        sh "git config user.name 'Jenkins CI'"
                        sh "git add values.yaml"
                        sh "git commit -m 'Update Docker tag to ${newTag}' || echo 'No changes to commit'"
                        sh "git push https://${GIT_USERNAME}:${GIT_TOKEN}@github.com/romain656/tp-devops.git HEAD:main"
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

