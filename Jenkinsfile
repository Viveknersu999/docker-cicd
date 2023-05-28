pipeline {
    agent any
    
    environment {
        //DOCKERHUB_USERNAME = 'vivek0991'
        DOCKERHUB_CREDENTIALS = credentials('docker')
        DOCKER_IMAGE_NAME = 'myweb_nginx01'
        DOCKERHUB_REPO = 'vivek0991/nginxapp'
        DOCKERFILE_PATH = '/var/lib/jenkins/workspace/dockerimage-deploy/Dockerfile'
	DOCKER_CONTAINER = 'my-first-nginx'
    }
    
    stages {
        stage('Welcome') { 
            steps { 
               echo 'This Build will create a Docker Container' 
            }
        }
        stage('Pull Sources') {
            steps {
		    git url: 'https://github.com/Viveknersu999/docker-cicd.git', branch: 'main'
		    //sh 'chmod +x /var/lib/jenkins/workspace/DockerImage/'
            }
         }
	 
	 stage('Build') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE_NAME .'
            }
        }
	
	stage('Push to Docker Hub') {
            steps {
		    sh 'docker run -d --name $DOCKER_CONTAINER -p 8070:80 $DOCKER_IMAGE_NAME'
		    sh 'docker ps'
                    sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR -p Saibaba@1609'
                    sh 'docker tag $DOCKER_IMAGE_NAME $DOCKERHUB_REPO'
            }
        }
        
	    
	      stage ('Deploy') {
          steps {
		  sh 'docker push $DOCKERHUB_REPO'
            	  echo 'Docker Image has been Successfully Pushed to Docker Hub'
                }
	    }  	       
    }
}
