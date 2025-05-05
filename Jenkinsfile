pipeline {
    agent any

    environment {
        SONARQUBE_ENV = 'SonarQube' // el nombre que configuraste en Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv("${SONARQUBE_ENV}") {
                    sh 'sonar-scanner -Dsonar.projectKey=my_project_key -Dsonar.sources=.'
                }
            }
        }
    }
}
