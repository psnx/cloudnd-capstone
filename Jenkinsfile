pipeline {
  agent any
  stages {
    
    stage('Linting Dockerfile') {
      steps {
        sh "docker run --rm -i hadolint/hadolint < Dockerfile"
      }
    }

    stage('Building image') {
      steps {
        script {
          dockerImage = docker.build image + ":$GIT_COMMIT"
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
        sh "docker rmi $image:$GIT_COMMIT"
      }
    }

    stage('Deploy') {
      steps {
        withAWS(region: 'eu-central-1', credentials: 'tamas') {
          sh '''
						kubectl config use-context arn:aws:eks:eu-central-1:174130021671:cluster/prod
            cat ./k8s/capstone.yml | sed 's/%TAG%/'"$GIT_COMMIT"'/g' | kubectl apply -f -
            # kubectl apply -f ./k8s/capstone.yml
            echo "image: $image:$GIT_COMMIT"
					'''
        }

      }
    }

  }
  environment {
    image = 'psnx/cloudnd-capstone'
    registryCredential = 'docker-hub'
    dockerImage = ''
  }
}