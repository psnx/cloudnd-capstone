pipeline {
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git(url: 'git@github.com:psnx/cloudnd-capstone.git', credentialsId: 'machine')
      }
    }

    stage('Building image') {
      steps {
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }

      }
    }

    stage('Deploy Image') {
      steps {
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }

      }
    }

    stage('Remove Unused docker image') {
      steps {
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }

  }
  environment {
    registry = 'psnx/cloudnd-capstone'
    registryCredential = 'dockerhub'
    dockerImage = ''
  }
}