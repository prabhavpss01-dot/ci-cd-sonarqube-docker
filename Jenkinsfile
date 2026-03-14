pipeline {
    agent any

    triggers {
        githubPush()
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/prabhavpss01-dot/ci-cd-sonarqube-docker.git'
            }
        }

        stage('Build') {
            steps {
                bat 'docker build -t ci-cd-sonarqube-docker .'
            }
        }

        stage('Test') {
            steps {
                bat 'pytest test\\test_app.py'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQubeServer') {
                    bat 'mvn sonar:sonar'
                }
            }
        }
    }
}
