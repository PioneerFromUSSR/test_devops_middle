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
               echo 'Building..'
               sh 'docker image build -t $DOCKER_HUB_REPO:latest .'
       }
   }
       stage('Docker Push') {
           steps {
               withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
               sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
               sh 'docker push $DOCKER_HUB_REPO:latest' 
       }
     }  
   }    
       stage('test') {
           steps {
               sh 'python test.py'
            }
           post {
               always {junit 'test-reports/*.xml'}
            }
       } 
 /*      stage('analyze') {
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
       } */
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
