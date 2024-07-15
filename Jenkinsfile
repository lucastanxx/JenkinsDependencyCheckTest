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
                // Correct the apiKey parameter to nvdApiKey
                dependencyCheck additionalArguments: '--nvdApiKey $NVD_API_KEY --format HTML --format XML --suppression suppression.xml', odcInstallation: 'OWASP Dependency-Check Vulnerabilities'
            }
        }
    }
    post {
        success {
            dependencyCheckPublisher pattern: 'dependency-check-report.xml'
        }
    }
}
