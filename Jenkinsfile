pipeline {
  environment {
    registry = "jkmathanmohan/test-docker-001"
 //    registryCredential = 'dockerhub'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/jkmathanmohan/docker-web-app.git'
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
//          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
//          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }
    stage (‘Deploy’) {
    sh ‘ssh ubuntu@10.0.1.46 mkdir -p /var/www/temp_deploy’
    }
  }
}
