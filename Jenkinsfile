pipeline {
    agent any
    environment {
        NVD_API_KEY = credentials('nvd-api-key-id')
    }
    stages {
        stage('Checkout SCM') {
            steps {
                git url: 'https://github.com/lucastanxx/JenkinsDependencyCheckTest.git', branch: 'master'
            }
        }

        stage('OWASP DependencyCheck') {
            steps {
                // Note the inclusion of apiKey in additionalArguments using the NVD_API_KEY environment variable
                dependencyCheck additionalArguments: '--apiKey $NVD_API_KEY --format HTML --format XML', odcInstallation: 'OWASP Dependency-Check Vulnerabilities'
            }
        }
    }
    post {
        success {
            dependencyCheckPublisher pattern: 'dependency-check-report.xml'
        }
    }
}
