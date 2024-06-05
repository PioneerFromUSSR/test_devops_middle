pipeline {
   agent any


   environment {
       DOCKER_HUB_REPO = "pioneerfromussr/flaskapp"
       CONTAINER_NAME = "flaskapp"

   }
   stages {
       stage('Checkout') {
           steps {
               checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/PioneerFromUSSR/test_devops_middle']]])
       }
   }
       stage('Docker build') {
           steps {
                sh 'docker image build -t $DOCKER_HUB_REPO:latest .'
                sh 'docker image tag $DOCKER_HUB_REPO:latest $DOCKER_HUB_REPO:$BUILD_NUMBER'
       }
   }
       stage('Docker push') {
           steps {
               withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
               sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
               sh 'docker push $DOCKER_HUB_REPO:$BUILD_NUMBER'
               sh 'docker push $DOCKER_HUB_REPO:latest' 
       }
     }  
   }    
       stage('test') {
           steps {
               sh '''
               cd /app
               sh 'python test.py'
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
