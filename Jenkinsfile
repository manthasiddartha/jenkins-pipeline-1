echo "Welcome to Pipeline"
pipeline {
    agent any
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
			   sh "mvn clean install -DskipTests"
			   echo "Completed creating jar file"
            }
        }
		stage("Docker build") {
     		steps {
			sh "USER 1000"
         		 sh "docker build -t currenyexchange ."
    		 }
			}
        stage("Deploy to staging") {
     		steps {
          sh "docker run -d --rm -p 8004:8004 -v /var/run/docker.sock:/var/run/docker.sock --privileged --name currenyexchange_1 currenyexchange"
     }
		}
    }
}
