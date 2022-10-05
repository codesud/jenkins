// pipeline {
//     agent any
//     parameters {
//         string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
//         text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
//         booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')
//         choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
//         password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
//     }

//     environment { 
//         ENV_URL = 'env.pipeline.com'
//     }

//     triggers { 
//         cron('H 11 * * *') 
//     }

//     triggers { 
//         pollSCM('H */4 * * 1-5') 
//     }
    
//     tools {
//         maven 'maven-2.0.10' 
//     }
    
//     stages {
//         stage('Stage One') {
//             environment { 
//             ENV_URL = 'env.stage.com' 
//             }
//             steps {
//                 sh 'echo ENV_URL = ${ENV_URL}'
//                 sh 'env'
//                 sh 'mvn --version'
//             }
//         }

//         stage('Stage Three') {
//             when {
//                 branch 'main'
//                 }
//             // when { 
//             //     environment name: 'CHOICE', value: 'One' 
//             //     }
//             steps {
//                 sh 'echo This stage is executed as this is the main branch'
//             }
//         }
//         stage('Stage Two') {
//             input {
//                 message "Are you sure you would like to continue? If yes, did you check with your DevOps Lead?"
//                 ok "Yes, I would like to continue"
//                 submitter "alice,bob"
//                 parameters {
//                     string(name: 'PERSON', defaultValue: 'DevOps Lead', description: 'Ensure you check with DevOps Lead')
//                 }
//             }
//             steps {
//                 echo 'Running the stage'
//             }
//         }

//     }
// }

pipeline {
    agent any
    stages {
        stage('Parallel Stage') {
            parallel {
                
                stage ('One') {
                    steps {
                        sh 'sleep 10'
                    }
                }

                stage ('Two') {
                    steps {
                        sh 'sleep 20'
                    }
                }
                
                stage ('Three') {
                    steps {
                        sh 'sleep 30'
                    }
                }
            }

        stage ('Four') {
                steps {
                    sh 'sleep 30'
                }
            }
        }
    }
}