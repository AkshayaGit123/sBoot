pipeline {
	agent any
	stages {
	    stage ('clean up') {
	        steps {
	            cleanWs()
	        }
	    }
	    stage ('clone') {
			steps {
				sh 'git clone https://github.com/AkshayaGit123/sBoot'
			}
		
		}
		stage ('build') {
			steps {
			    dir ('sBoot'){
				    sh 'mvn clean install -DskipTests'
			    }
			}
		}
		stage ('test') {
			steps {
			    dir ('sBoot'){
				    sh 'mvn test'
			    }
			}
			post {
				always {
				    dir ('sBoot'){
					    junit 'target/surefire-reports/*.*xml'
					    archiveArtifacts artifacts: 'target/*.war', followSymlinks: false
				    }
				}
			}
		}
		stage ('run') {
			steps {
			    dir ('sBoot'){
			    	sh 'mvn clean package'

			    }
			}
		
		}
	
	}
}
