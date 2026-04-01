pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('SonarQube Analysis') {
            environment {
                SONAR_TOKEN = credentials('sonarqube-token')
            }
            steps {
                sh '''
                  /opt/sonar-scanner/bin/sonar-scanner \
                    -Dsonar.projectKey=longchain_python \
                    -Dsonar.sources=. \
                    -Dsonar.host.url=http://localhost:9000 \
                    -Dsonar.login=$SONAR_TOKEN
                '''
            }
        }
    }
}
