pipeline {
    agent any
	
	  tools
    {
       maven "Maven"
    } 
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/bala3404/CI-CD-using-Docker.git'
             
          }
        }
	 stage('Execute Maven') {
           steps {
             
                sh 'mvn package'             
          }
        }
        

  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t samplewebapp:latest .' 
                sh 'docker tag samplewebapp bala3404/samplewebapp:latest'
                //sh 'docker tag samplewebapp bala3404/samplewebapp:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "dockerhub_id", url: "" ]) {
          sh  'docker push bala3404/samplewebapp:latest'
        //  sh  'docker push bala3404/samplewebapp:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -d -p 8003:8080 bala3404/samplewebapp"
 
            }
         }
      }
    }
