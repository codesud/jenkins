pipeline {
    agent any
    stages {
        stage('Stage One') {
            steps {
                echo 'Hello World'
            }
        }
        stage('Stage Two') {
            steps {
                echo 'Hello Cloud'
            }
        }
        stage('Stage Three') {
            steps {
                sh '''
                echo "Hai"
                echo "Welcome to DevOps"
                echo " In CICD, Jenkins is top notch"
                '''                
            }
        }
    }
}

