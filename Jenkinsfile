echo "Welcome to Pipeline"
pipeline {
	sudo su 
	sudo yum install docker-engine -y
	sudo service docker start
    agent { dockerfile true }
	environment{ 
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
    stages { 
        stage('Build') {
            steps { 
               echo "Build"
			   echo "PATH -$PATH"
            }
        }
        stage('Test') {
            steps { 
                echo "Test"
            }
        }
		stage('Package') {
            steps { 
               echo "Started creating jar file"
			   sh "mvn package -DskipTests"
			   echo "Completed creating jar file"
            }
        }
        stage('Deploy') {
            steps {
               echo "Deploy"
            }
        }
    }
}