pipeline {
    agent any

    environment {
        SONARQUBE = 'SonarQube' // Ensure this matches the name in Jenkins configuration
    }

    stages {
        stage('Checkout SCM') {
            steps {
                git 'https://github.com/ivanlsy/JenkinsDependencyCheckTest.git'
            }
        }

        stage('Code Quality Check via SonarQube') {
            steps {
                script {
                    def scannerHome = tool 'SonarQubeScanner'
                    withSonarQubeEnv('SonarQube') {
                        sh "${scannerHome}/bin/sonar-scanner"
                    }
                }
            }
        }
    }

    post {
        always {
            recordIssues tool: sonarQube(pattern: '**/sonar-report.json')
        }
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
