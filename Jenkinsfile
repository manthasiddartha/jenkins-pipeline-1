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
		
		
	    stage("Connect to Gcloud"){
		    steps{
		     sh 'gcloud auth activate-service-account --key-file=symbolic-card-270810-cea46baeb61d.json'
		     sh 'gcloud container clusters get-credentials cluster-1 --zone us-central1-c --project symbolic-card-270810'
                     sh 'kubectl get pods'
		    }
	    }
    }
}
