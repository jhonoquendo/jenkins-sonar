pipeline {
    agent any

    tools {
        nodejs "NodeJs" // ← exacto al nombre que configuraste en Jenkins
    }

    environment {
        SONAR_TOKEN = credentials('sonarqube-token') // ID de la credencial en Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install') {
            steps {
                sh 'npm install'
                sh 'npm install -g sonar-scanner' 
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') { // Nombre del servidor en Jenkins
                    sh '''
                        sonar-scanner \
                          -Dsonar.projectKey=jenkins-sonar \
                          -Dsonar.sources=. \
                          -Dsonar.login=${SONAR_TOKEN}
                    '''
                }
            }
        }

        stage('Quality Gate') {
            steps {
                timeout(time: 1, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}
