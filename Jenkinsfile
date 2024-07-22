pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                // Checkout the code from your repository
                git url: 'https://github.com/ivanlsy/JenkinsDependencyCheckTest.git', branch: 'master'
            }
        }

        stage('OWASP Dependency-Check Vulnerabilities') {
            steps {
                dependencyCheck additionalArguments: '''
                -o ./dependency-check-report
                -s .
                -f ALL
                --prettyPrint''', odcInstallation: 'OWASP Dependency-Check Vulnerabilities'
            }
        }
    }
    
    post {
        success {
            dependencyCheckPublisher pattern: 'dependency-check-report/dependency-check-report.xml'
        }
    }
}
