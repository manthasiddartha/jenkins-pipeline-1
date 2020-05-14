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
			sh "helm version"
    		 }
			}
		
		
	    stage("Connect to Gcloud"){
		    agent{
 			label 'gcloud'
		    }
		    steps{
		     sh 'gcloud auth activate-service-account --key-file=symbolic-card-270810-493a984c2e58.json'
		     sh 'gcloud container clusters get-credentials cluster-1 --zone us-central1-c --project symbolic-card-270810'
                     sh 'kubectl create -f deployment-info.yaml'
		    }
	    }
    }
}
