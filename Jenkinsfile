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
        cron('H 11 * * *') 
    }

    // triggers { 
    //     pollSCM('H */4 * * 1-5') 
    // }
    
    tools {
        maven 'maven-2.0.10' 
    }
    
    stages {
        stage('Stage One') {
            environment { 
            ENV_URL = 'env.stage.com' 
            }
            steps {
                sh 'echo ENV_URL = ${ENV_URL}'
                sh 'env'
                sh 'mvn --version'
            }
        }
        stage('Stage Two') {
            input {
                message "Are you sure you would like to continue? If yes, did you check with your DevOps Lead?"
                ok "Yes, we should."
                submitter "alice,bob"
                parameters {
                    string(name: 'PERSON', defaultValue: 'DevOps Lead', description: 'Who should I say hello to?')
                }
            }
            steps {
                echo "Hello, ${PERSON}, nice to meet you."
            }
        }

    }
}