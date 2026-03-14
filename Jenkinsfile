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
                sh 'docker build -t ci-cd-sonarqube-docker .'
            }
        }

        stage('Test') {
            steps {
                sh 'pytest test/'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('MySonarQubeServer') {
                    sh 'mvn sonar:sonar'
                }
            }
        }
    }
}
