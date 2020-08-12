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
        
    }
}
