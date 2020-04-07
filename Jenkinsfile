pipeline {
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

    stage('Deploy') {
      steps {
        withAWS(region: 'eu-central-1', credentials: 'tamas') {
          sh '''
						kubectl config use-context arn:aws:eks:eu-central-1:174130021671:cluster/prod
            cat ./k8s/capstone.yml | sed 's/%TAG%/'"$BUILD_NUMBER"'/g' | kubectl apply -f -
					'''
        }

      }
    }

  }
  environment {
    registry = 'psnx/cloudnd-capstone'
    registryCredential = 'docker-hub'
    dockerImage = ''
  }
}