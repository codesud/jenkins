pipeline {
    agent any
    environment { 
        ENV_URL = 'env.pipeline.com'
    }
    stages {
        stage('Stage One') {
            steps {
                echo 'Hello World'
            }
        }
        stage('Stage Two') {
            steps {
                sh "echo ENV_URL = ${ENV_URL}"

            }
        }

    }
}

