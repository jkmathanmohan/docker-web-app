pipeline {
  environment {
    registry = "jkmathanmohan/test-docker-001"
     registryCredential = 'dockerhub'
    dockerImage = ''
  }
  agent any
  stages {
   //Git Cloning from github
    stage('Cloning Git') {
      steps {
        git 'https://github.com/jkmathanmohan/docker-web-app.git'
      }
    }
    stage('Building image') {
      //Build docker image 
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Deploy Image') {
      //Push the docker image to dockerhub
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
           }
        }
      }
    }
    stage('Remove Unused docker image') {
      //Remove Unused docker images
      steps{
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }
    stage ('Deploy') {
      //Deploy the docker image into EC2 instance
      steps{
        sh "ssh  ubuntu@10.0.1.46 sudo docker stop mytestproject"
        sh "ssh  ubuntu@10.0.1.46 sudo docker rm mytestproject"
        sh "ssh  ubuntu@10.0.1.46 sudo docker pull $registry:$BUILD_NUMBER"
        sh "ssh  ubuntu@10.0.1.46 sudo docker run -d --name mytestproject -p 8080:8080 $registry:$BUILD_NUMBER"
      }
      //email notification
      post {
        always {
           emailext (
      subject: '$registry:$BUILD_NUMBER', 
     mimetype: 'text/html', 
     to: 'jkmathanmohan@gmail.com',
     recipientProviders: [[$class: 'CulpritsRecipientProvider'],[$class: 'RequesterRecipientProvider']], 
     body: 'A Docker Deploy Complete'
    )
      }
     }
    }
  }
}
