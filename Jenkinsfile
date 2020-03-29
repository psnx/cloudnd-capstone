pipeline {
    agent any 
    stages {
        stage('Source'){
            git 'git@github.com:psnx/cloudnd-capstone.git'
        }
        
        stage('Build') {
            agent {
                docker {
                    image 'capstone'
                    label 'v1'
                    registryUrl 'https://hub.docker.com/psnx/'
                    registryCredentialsId 'docker-hub'
                }
            }
        }
        stage('Test') { 
            steps {
                sh 'echo "Testing stage"'
            }
        }
        stage('Deploy') { 
            steps {
                sh 'echo "Deployment stage"'
            }
        }
    }
}