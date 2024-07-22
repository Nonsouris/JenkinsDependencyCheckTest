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
				dependencyCheck additionalArguments: '--format HTML --format XML --nvdApiKey 4314dcc0-a7e3-44eb-a1be-423b66d4f4b1', odcInstallation: 'OWASP Dependency-Check Vulnerabilities'
			}
		}
	}	
	post {
		success {
			dependencyCheckPublisher pattern: 'dependency-check-report.xml'
		}
	}
}