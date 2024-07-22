pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                // Ensure this points to your remote repository
                git 'https://github.com/ivanlsy/JenkinsDependencyCheckTest.git'
            }
        }

        stage('OWASP Dependency-Check Vulnerabilities') {
            steps {
                dependencyCheck additionalArguments: '''
                -o ./dependency-check-report
                -s .
                -f 'ALL'
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
