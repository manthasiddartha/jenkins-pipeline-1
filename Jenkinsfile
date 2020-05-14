echo "Welcome to Pipeline"
pipeline {
    agent any
	environment{ 
		mavenHome = tool 'myMaven'
		PATH = "$mavenHome/bin:$PATH"
	}
    stages { 
        stage('Build') {
            steps { 
               echo "Build"
			   echo "PATH -$PATH"
		          sh "gcloud version"
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
         		 sh "docker build -t currenyexchange ."
    		 }
			}
		
		
        stage("Deploy to staging") {
     		steps {
          sh "docker run -d --rm -p 9001:9001 -v /var/run/docker.sock:/var/run/docker.sock --privileged --name currenyexchange_1 currenyexchange"
     }
		}
	    stage("Connect to Gcloud"){
		    steps{
		     sh 'gcloud auth activate-service-account --key-file=#SERVICE ACCOUNT NOW'
        	     sh 'FILL CLUTSTER CONNECT ISSUE'
                     sh 'kubectl apply -f deploy-info.yaml'
                     sh 'kubectl apply -f service-info.yaml'
		    }
	    }
    }
}
