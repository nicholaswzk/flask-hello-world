pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                echo "test"
            }
        }
        stage('OWASP Dependency Check') {
			steps {
			    echo '-------- Performing OWASP Dependency Check --------'
				dependencyCheck additionalArguments: '--disableYarnAudit --format HTML --format XML', odcInstallation: 'Default'
				dependencyCheckPublisher pattern: 'dependency-check-report.xml'
                echo "OWASP DependencyCheck has no errors! Proceeding on!"
			}
		}
		stage('SonarQube Analysis') {
            steps {
                script {
                    echo '-------- Performing SonarQube Scan --------'
                    def scannerHome = tool 'SonarQube';
                    withSonarQubeEnv('SonarQube') {
                        sh "${scannerHome}/bin/sonar-scanner"
                    }
                       echo "SonarQube Analysis has no errors! Proceeding on!"
                }
            }
        }
		
  }
    }
