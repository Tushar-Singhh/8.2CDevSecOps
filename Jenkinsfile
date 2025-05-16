pipeline {
    agent any

    tools {
        nodejs 'NodeJS 18'  // Make sure this matches your Jenkins NodeJS setup
    }

    environment {
        SONAR_TOKEN = credentials('your-sonar-token-id')  // Replace with your Jenkins credentials ID
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Tushar-Singhh/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test || true'
            }
        }

        stage('Generate Coverage Report') {
            steps {
                sh 'npm run coverage || true'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                sh 'npm audit || true'
            }
        }

        stage('SonarQube Scan') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh "sonar-scanner \
                        -Dsonar.projectKey=8.2CDevSecOps \
                        -Dsonar.sources=. \
                        -Dsonar.host.url=https://sonarcloud.io \
                        -Dsonar.login=$SONAR_TOKEN"
                }
            }
        }
    }
}

