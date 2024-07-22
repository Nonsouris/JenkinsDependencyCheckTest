pipeline {
	agent any
	stages {
		stage('Checkout SCM') {
			steps {
                checkout([$class: 'GitSCM', 
						branches: [[name: '*/master']], 
						userRemoteConfigs: [[
							url: 'https://github.com/Nonsouris/JenkinsDependencyCheckTest' 
						]]
						])
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