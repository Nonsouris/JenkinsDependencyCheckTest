pipeline {
	agent any
	stages {
		stage('Checkout SCM') {
			steps {
                checkout([$class: 'GitSCM', 
						branches: [[name: '*/master']], // Replace with your branch name
						doGenerateSubmoduleConfigurations: false,
						extensions: [],
						userRemoteConfigs: [[
							url: 'https://github.com/Nonsouris/JenkinsDependencyCheckTest', // Replace with your repo URL
							\\credentialsId: "${GITHUB_CREDENTIALS}"
						]]
			}
		}

		stage('OWASP DependencyCheck') {
			steps {
				dependencyCheck additionalArguments: '--format HTML --format XML', odcInstallation: 'Default'
			}
		}
	}	
	post {
		success {
			dependencyCheckPublisher pattern: 'dependency-check-report.xml'
		}
	}
}