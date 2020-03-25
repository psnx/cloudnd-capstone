pipeline {
    agent any 
    stages {
        stage('Build') { 
            steps {
                sh 'echo Linting HTML'
                sh 'tidy -q -e *.html' 
            }
        }
        stage('Test') { 
            steps {
                // 
            }
        }
        stage('Deploy') { 
            steps {
                // 
            }
        }
    }
}