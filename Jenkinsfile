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
    
    stage('Set current kubectl context') {
			steps {
				withAWS(region:'eu-central-1', credentials:'eks-admin') {
					sh '''
						kubectl config use-context arn:aws:eks:eu-central-1:174130021671:cluster/prod
					'''
				}
			}
		}

    stage('Deploy blue container') {
			steps {
				withAWS(region:'eu-central-1', credentials:'eks-admin') {
					sh '''
						kubectl apply -f k8s/capstone.yml
					'''
				}
			}
		}
  }
}
