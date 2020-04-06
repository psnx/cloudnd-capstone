pipeline {
    environment {
    registry = 'psnx/cloudnd-capstone'
    registryCredential = 'docker-hub'
    dockerImage = ''
    }
  agent {
  kubernetes {
      label 'cloudnd-capstone'
      idleMinutes 5  // how long the pod will live after no jobs have run on it
      yamlFile 'k8s/capstone.yml'  // path to the pod definition relative to the root of our project 
      defaultContainer 'capstone'  // define a default container if more than a few stages use it, will default to jnlp container
    }
  }
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
				withAWS(region:'eu-central-1', credentials:'tamas') {
					sh '''
						kubectl config use-context arn:aws:eks:eu-central-1:174130021671:cluster/prod
					'''
				}
			}
		}

    stage('Deploy blue container') {
			steps {
				withAWS(region:'eu-central-1', credentials:'tamas') {
					sh '''
						kubectl apply -f ./k8s/capstone.yml
					'''
				}
			}
		}

  }
}
