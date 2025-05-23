pipeline {
    agent any

    environment {
        SONARQUBE = 'SonarQubeServer'        // Nom utilisé dans la config Jenkins
        DOCKER_IMAGE = 'romain656/tp-devops' // Nom de ton repo DockerHub
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building...'
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing...'
                // Ajoute ici des tests si besoin
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv("${SONARQUBE}") {
                    sh 'sonar-scanner -Dsonar.projectKey=tp-devops -Dsonar.sources=. -Dsonar.java.binaries=.'
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                script {
                    docker.withRegistry('', 'dockerhub-creds') {
                        docker.image("$DOCKER_IMAGE").push('latest')
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying...'
            }
        }
    }
}
