pipeline {
    agent any
	environment { 
        mvnHome = tool 'Maven_Config'
    }
    stages {
		stage('Preparation') {
			steps {
				git url: 'https://github.com/CA-MMISDigitalServices/Dev.git', branch: 'master'
			}
		}
        stage('Build') {
            steps {
			sh "'${mvnHome}/bin/mvn' -X -B --file /var/lib/jenkins/workspace/TestPipeline/SpringPOC -Dmaven.test.failure.ignore clean install"
                }
            post {
                always {
                    echo '******************* always'
                }
		failure {
			echo '****************** failure'
		}
		success {
			echo '****************** success'
		}
            }
        }
        stage('Test') { 
            steps {
                junit '**/target/surefire-reports/*.xml'
            }
            post {
                always {
                 	echo 'always'
                }
		changed {
		 	echo 'change'
		}
		aborted {
			echo 'aborted'
		}
		failure {
			echo 'failure'
		}
		success {
			echo 'success'
		}
		unstable {
			echo 'unstable'
		}
            }
        }
    }
}
