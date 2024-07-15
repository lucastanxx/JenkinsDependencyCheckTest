pipeline {
	agent any
	stages {
		stage('Checkout SCM') {
			steps {
                git url: 'https://github.com/donhitme34/JenkinsDependencyCheckTest.git', branch: 'master'
			}
		}

		stage('OWASP DependencyCheck') {
			steps {
                dependencyCheck additionalArguments: '--format HTML --format XML', odcInstallation: 'OWASP Dependency-Check Vulnerabilities'
			}
		}
	}	
	post {
		success {
			dependencyCheckPublisher pattern: 'dependency-check-report.xml'
		}
	}
}
