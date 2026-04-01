pipeline {
    agent any

    stages {

        stage('Checkout Source Code') {
            steps {
                git url: 'https://github.com/RETHANYA10/longchain_python.git', branch: 'main'
            }
        }

        stage('Show Workspace Files') {
            steps {
                sh '''
                echo "===== FILES IN WORKSPACE ====="
                ls -l
                '''
            }
        }

        stage('SonarQube Scan') {
            steps {
                sh '''
                echo "===== RUNNING SONARQUBE SCAN ====="

                /opt/sonar-scanner/bin/sonar-scanner \
                  -Dsonar.projectKey=new_sonar \
                  -Dsonar.sources=. \
                  -Dsonar.host.url=http://localhost:9000 \
                  -Dsonar.login=sqp_7fa7154bfca0ea5fa5da841bdfa51fa124a9d34c
                '''
            }
        }
    }

    post {
        success {
            echo '✅ SonarQube analysis completed SUCCESSFULLY'
        }
        failure {
            echo '❌ SonarQube analysis FAILED'
        }
    }
}
``
