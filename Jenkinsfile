pipeline {
    agent any 
    stages {
        stage('Build') { 
            steps {
                sh 'Building stage'
                sh 'tidy -q -e *.html' 
            }
        }
        stage('Test') { 
            steps {
                sh 'Testing stage'
            }
        }
        stage('Deploy') { 
            steps {
                sh 'Deployment stage'
            }
        }
    }
}