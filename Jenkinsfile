pipeline {
    agent any
    environment { 
        ENV_URL = 'env.pipeline.com'
    }
    stages {
        stage('Example Username/Password') {
            environment {
                SERVICE_CREDS = credentials('my-predefined-username-password')
            }
            steps {
                sh 'echo "Service user is $SERVICE_CREDS_USR"'
                sh 'echo "Service password is $SERVICE_CREDS_PSW"'
                sh 'curl -u $SERVICE_CREDS https://myservice.example.com'
            }

       stage('Stage One') {
            steps {
                sh "echo 'Hello World'"
            }
        }
       stage('Stage Two') {
            steps {
                sh "echo 'Hello DevOps'"
            }
        }
        stage('Stage Three') {
            environment { 
            ENV_URL = 'env.stage.com' 
            }
            steps {
                sh "echo ENV_URL = ${ENV_URL}"
            }
        }

    }
}