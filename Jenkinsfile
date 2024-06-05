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
       stage('Build') {
           steps {
               echo 'Building..'
               sh 'docker image build -t $DOCKER_HUB_REPO:latest .'
               script {
               def image = docker.build('$DOCKER_HUB_REPO:latest')
               image.push()
               }
       }
   }
       stage('analyze') {
            steps {
                sh 'echo "$DOCKER_HUB_REPO:latest `pwd`/Dockerfile" > anchore_images'
                anchore name: 'anchore_images'
            }
       }
       stage('teardown') {
           steps {
               sh'''
                   for i in `cat anchore_images | awk '{print $1}'`;do docker rmi $i; done
               '''
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
