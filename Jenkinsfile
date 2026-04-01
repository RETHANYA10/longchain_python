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
                withCredentials([string(credentialsId: 'sonarqube-token', variable: 'SONAR_TOKEN')]) {
                    sh '''
                    echo "===== RUNNING SONARQUBE SCAN ====="

                    /opt/sonar-scanner/bin/sonar-scanner \
                      -Dsonar.projectKey=new_sonar \
                      -Dsonar.projectName=new_sonar \
                      -Dsonar.sources=. \
                      -Dsonar.host.url=http://localhost:9000 \
                      -Dsonar.login=$SONAR_TOKEN
                    '''
                }
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
