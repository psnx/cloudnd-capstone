pipeline {
    agent any 
    stages {
        stage('Build') { 
            steps {
                sh 'echo "Building stage"'
                sh 'tidy -q -e *.html' 
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