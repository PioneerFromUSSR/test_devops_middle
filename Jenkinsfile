pipeline {
   agent any


   environment {
       DOCKER_HUB_REPO = "pioneerfromussr/flaskapp"
       CONTAINER_NAME = "flaskapp"

   }

   stage('Checkout') {
       steps {
           checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConf
       }
   }
   stage('Build') {
       steps {
           echo 'Building..'
           sh 'docker image build -t $DOCKER_HUB_REPO:latest .'
       }
   }
   stage('Deploy') {
       steps {
           echo 'Deploying..'
           sh 'docker stop $CONTAINER_NAME || true'
           sh 'docker rm $CONTAINER_NAME || true'
           sh 'docker run -d -p 80:8080 --name $CONTAINER_NAME $DOCKER_HUB_REPO'
       }
   }
 }
} 
