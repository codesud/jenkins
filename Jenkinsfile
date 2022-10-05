pipeline {
    agent any
    environment { 
        ENV_URL = 'env.pipeline.com'
    }
    stages {
        stage('Example Username/Password') {
            environment {
                SSH_CREDS = credentials('SSH-Centos7')
            }
            steps {
                sh 'echo "SSH private key is located at $SSH_CREDS"'
                sh 'echo "SSH user is $SSH_CREDS_USR"'
                sh 'echo "SSH password is $SSH_CREDS_PSW"'
            }
        }
        stage('Stage One') {
            steps {
                sh 'echo "Hello World"'
            }
        }
        stage('Stage Two') {
            steps {
                sh 'echo "Hello DevOps"'
            }
        }
        stage('Stage Three') {
            environment { 
            ENV_URL = 'env.stage.com' 
            }
            steps {
                sh 'echo ENV_URL = ${ENV_URL}'
                sh 'env'
            }
        }

    }
}