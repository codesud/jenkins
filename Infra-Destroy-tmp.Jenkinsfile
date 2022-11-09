pipeline {
    agent any
    parameters
         { 
            choice(name: 'ENV', choices: ['dev', 'prod'], description: 'ENV')
            string(name: 'APP_VERSION', defaultValue: '', description: 'Just give dummy value - Ignore this VPC ALB and DB')     
          }
   
    stages {
         stage('Backend-1') {
            parallel {
               stage('Deleting-User') {
                   steps {
                       dir('USER') {  git branch: 'main', url: 'https://github.com/codesud/user.git'
                          sh '''
                            cd terraform-mutable
                            export TF_VAR_APP_VERSION=3.0.0
                            terrafile -f env-${ENV}/Terrafile
                            terraform init -backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure
                            terraform plan -var-file=env-${ENV}/${ENV}.tfvars
                            terraform destroy -var-file=env-${ENV}/${ENV}.tfvars -auto-approve
                          '''
                            }
                        }
                   }
               stage('Deleting-Catalogue') {
                   steps {
                       dir('Catalogue') {  git branch: 'main', url: 'https://github.com/codesud/catalogue.git'
                          sh '''
                            sleep 40
                            cd terraform-mutable
                            export TF_VAR_APP_VERSION=3.0.0
                            terrafile -f env-${ENV}/Terrafile
                            terraform init -backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure
                            terraform plan -var-file=env-${ENV}/${ENV}.tfvars
                            terraform destroy -var-file=env-${ENV}/${ENV}.tfvars -auto-approve
                          '''
                            }
                        }
                  }
            stage('Deleting-Payment') {
                steps {
                    dir('PAYMENT') {  git branch: 'main', url: 'https://github.com/codesud/payment.git'
                          sh '''
                            sleep 90
                            cd terraform-mutable
                            export TF_VAR_APP_VERSION=3.0.0
                            terrafile -f env-${ENV}/Terrafile
                            terraform init -backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure
                            terraform plan -var-file=env-${ENV}/${ENV}.tfvars
                            terraform destroy -var-file=env-${ENV}/${ENV}.tfvars -auto-approve
                          '''
                         }
                     }
                }
          stage('Deleting-Cart') {
                steps {
                    dir('CART') {  git branch: 'main', url: 'https://github.com/codesud/cart.git'
                          sh '''
                            cd terraform-mutable
                            export TF_VAR_APP_VERSION=3.0.0
                            terrafile -f env-${ENV}/Terrafile
                            terraform init -backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure
                            terraform plan -var-file=env-${ENV}/${ENV}.tfvars
                            terraform destroy -var-file=env-${ENV}/${ENV}.tfvars -auto-approve
                          '''
                         }
                     }
                }
            stage('Deleting-Shipping') {
                steps {
                    dir('SHIPPING') {  git branch: 'main', url: 'https://github.com/codesud/shipping.git'
                          sh '''
                            cd terraform-mutable
                            export TF_VAR_APP_VERSION=3.0.0
                            terrafile -f env-${ENV}/Terrafile
                            terraform init -backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure
                            terraform plan -var-file=env-${ENV}/${ENV}.tfvars
                            terraform destroy -var-file=env-${ENV}/${ENV}.tfvars -auto-approve
                          '''
                         }
                     }
                }
            stage('Deleting-Frontend') {
                       steps {
                           dir('FRONTEND') {  git branch: 'main', url: 'https://github.com/codesud/frontend.git'
                              sh '''
                                pwd ; ls -ltr
                                cd ./terraform-mutable
                                export TF_VAR_APP_VERSION=3.0.0
                                terrafile -f env-${ENV}/Terrafile
                                terraform init -backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure
                                terraform plan -var-file=env-${ENV}/${ENV}.tfvars
                                terraform destroy -var-file=env-${ENV}/${ENV}.tfvars -auto-approve
                              '''
                                }
                            }
                       }
             } // Parallel Stages Completed
          }   // Stage Completed

       stage('DB-n-ALB') {
        parallel {
        stage('Deleting-DB') {
            steps {
            dir('EC2') { git branch: 'main', url:'https://github.com/codesud/terraform-databases.git'
                       sh "ls -ltr"
                       sh "export TF_VAR_APP_VERSION=3.0.0"
                       sh "terrafile -f env-${ENV}/Terrafile"
                       sh "terraform init -backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure"
                       sh "terraform plan -var-file=env-${ENV}/${ENV}.tfvars"
                       sh "terraform destroy -auto-approve -var-file=env-${ENV}/${ENV}.tfvars || true"
                       sh "terraform destroy -auto-approve -var-file=env-${ENV}/${ENV}.tfvars"
                    }
               }
        }
        stage('Deleting-ALB') {
            steps {
                dir('VPC') {  git branch: 'main', url: 'https://github.com/codesud/tf-loadbalancers.git'
                        sh "ls -ltr"
                        sh "terrafile -f env-${ENV}/Terrafile"
                        sh "terraform init -backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure"
                        sh "terraform plan -var-file=env-${ENV}/${ENV}.tfvars"
                        sh "terraform destroy -auto-approve -var-file=env-${ENV}/${ENV}.tfvars"
                        }
                    }
                }
            }   // Closure of parallel stages
        }   // parallel completed
        
        stage('Deleting-VPC') {
            steps {
                dir('VPC') {  git branch: 'main', url: 'https://github.com/codesud/terraform-vpc.git'
                        sh "ls -ltr"
                        sh "export TF_VAR_APP_VERSION=3.0.0"
                        sh "terrafile -f env-${ENV}/Terrafile"
                        sh "terraform init -backend-config=env-${ENV}/${ENV}-backend.tfvars"
                        sh "terraform plan -var-file=env-${ENV}/${ENV}.tfvars"
                        sh "terraform destroy -auto-approve -var-file=env-${ENV}/${ENV}.tfvars"
                     }
                 }
            }       
        }
    }