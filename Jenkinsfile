pipeline {
    agent any

    environment {
        SONARQUBE_ENV = 'SonarQubeServer'
        DOCKER_IMAGE = 'springboot-app'
    }

    stages {
        stage('Checkout') {
            steps { git 'https://github.com/GharianiAziz/devops2.git' }
        }
        stage('Maven Build') {
            steps { sh 'mvn clean install' }
        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv("${SONARQUBE_ENV}") {
                    sh 'mvn sonar:sonar'
                }
            }
        }
        stage('Docker Build') {
            steps { sh 'docker build -t $DOCKER_IMAGE .' }
        }
    }

    post {
        success { echo '✅ Pipeline réussi' }
        failure { echo '❌ Pipeline échoué' }
    }
}
