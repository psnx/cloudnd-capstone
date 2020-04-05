pipeline {
    environment {
    registry = 'psnx/cloudnd-capstone'
    registryCredential = 'docker-hub'
    dockerImage = ''
    }
  agent any
  stages {
    stage('Building image') {
      steps {
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }

      }
    }

    stage('Push Image') {
      steps {
        script {
          docker.withRegistry('', registryCredential ) {
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

    stage('Deploy'){
      steps {
        sh "/usr/local/bin/kubectl apply -f ./k8s/deployment"
        sh "/usr/local/bin/kubectl get svc"
      }
    }

  }
  
}
