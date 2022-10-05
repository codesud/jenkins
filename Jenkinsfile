pipeline {
    agent any
    parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')

        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')

        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')

        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')

        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    }

    environment { 
        ENV_URL = 'env.pipeline.com'
    }

    triggers { 
        cron('0 11 * * *') 
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