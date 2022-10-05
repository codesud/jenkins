pipeline {
    agent any
    environment { 
        ENV_URL = 'env.pipeline.com'
    }
    stages {
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

