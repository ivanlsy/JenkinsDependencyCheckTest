pipeline {
    agent any
    
    environment {
        // Define the SonarQube server URL and token
        SONARQUBE_SERVER = 'http://172.30.137.160:9000/'
        SONARQUBE_TOKEN = 'sqp_70b294e68345dbfdb2105d7d271169eabfab8649'
    }
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/2201656/Vulnerable-Web-Application.git'
            }
        }
        
        stage('Code Quality Check via SonarQube') {
            steps {
                script {
                    def scannerHome = tool 'SonarQube';
                    withSonarQubeEnv('SonarQube') {
                        sh """
                        ${scannerHome}/bin/sonar-scanner \
                        -Dsonar.projectKey=OWASP \
                        -Dsonar.sources=. \
                        -Dsonar.host.url=${env.SONARQUBE_SERVER} \
                        -Dsonar.login=${env.SONARQUBE_TOKEN} \
                        -Dsonar.verbose=true -X
                        """
                    }
                }
            }
        }
    }
    
    post {
        always {
                recordIssues enabledForFailure: true, tool: sonarQube()
            }
        }
    }