pipeline {
  environment {
    registry = "haobug/hello_world_web_application"
    registryCredential = 'dockerhub'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        echo 'Pulling from Github'
        git 'https://github.com/transferhp/cicd-demo.git'
      }
    }
    stage('Building image') {
      steps{
        echo 'Building hello_world_web_applicaiton image'
        script {
          dockerImage = docker.build(registry + ":$BUILD_NUMBER", "./hello_world_web_application/")
        }

        echo 'Building jenkins-docker image'
        script {
          dockerImage = docker.build(registry + ":$BUILD_NUMBER", "./jenkins-docker/")
        }
      }
    }
    stage('Deploy Image') {
      steps{
        echo "Deploy Image to Dockerhub"
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        echo "Remove Unused docker image"
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }
  }
}