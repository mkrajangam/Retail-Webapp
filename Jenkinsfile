currentBuild.displayName = "Online-Shopping-#"+currentBuild.number
pipeline {
    agent any
	
	environment {
		PATH = "/usr/share/maven/bin:$PATH"
	
	}

    stages {
        stage("Git Checkout") {
            steps {
                git 'https://github.com/mkrajangam/Retail-Webapp'
            }
        }
        stage("Maven Build") {
            steps {
                sh "mvn clean package"
            }
        }
        stage("deploy-dev") {
            steps {
				sshagent(['deploy-dev']) { 
				sh """
					scp -o StrictHostKeyChecking=no target/retailone.war devops@192.168.5.129:/opt/tomcat/webapps/
					ssh devops@192.168.5.129 /opt/tomcat/bin/shutdown.sh
					ssh devops@192.168.5.129 /opt/tomcat/bin/startup.sh
				"""
				}
                
            }
        } 
    }
	post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}

