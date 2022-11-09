pipeline {
    agent any
    parameters
         { 
            choice(name: 'ENV', choices: ['dev', 'prod'], description: 'ENV')
            string(name: 'APP_VERSION', defaultValue: '', description: 'Choose App Version To Deploy : Ignore this VPC ALB and DB')
     
          }
    stages {
        stage('Creating-VPC') {
            steps {
                dir('VPC') {  git branch: 'main', url: 'https://github.com/codesud/terraform-vpc.git'
                        sh "ls -ltr"
                        sh "export TF_VAR_APP_VERSION=3.0.0"
                        sh "terrafile -f env-${ENV}/Terrafile"
                        sh "terraform init -backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure"
                        sh "terraform plan -var-file=env-${ENV}/${ENV}.tfvars"
                        sh "terraform apply -auto-approve -var-file=env-${ENV}/${ENV}.tfvars"
                     }
                 }
            }
     stage('DB-n-EKS') {
        parallel {
        stage('Creating-DB') {
            steps {
            dir('EC2') { git branch: 'main', url:'https://github.com/codesud/terraform-databases.git'
                       sh "ls -ltr"
                       sh "export TF_VAR_APP_VERSION=3.0.0"
                       sh "terrafile -f env-${ENV}/Terrafile"
                       sh "terraform init -backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure"
                       sh "terraform plan -var-file=env-${ENV}/${ENV}.tfvars"
                       sh "terraform apply -auto-approve -var-file=env-${ENV}/${ENV}.tfvars || true"
                       sh "terraform apply -auto-approve -var-file=env-${ENV}/${ENV}.tfvars"
                    }
               }
        }
        stage('Creating-EKS') {
            steps {
                dir('EKS') {  git branch: 'main', url: 'https://github.com/codesud/kubernetes.git'

                        sh ''' 
                            cd eks 
                            ls -ltr 
                            make create
                            aws eks update-kubeconfig  --name dev-eks-cluster
                            kubectl get nodes
                        ''' 
                     }
                 }
            }
        }   // Closure of parallel stages
    }   // parallel completed

         stage('Backend') {
            parallel {
               stage('Creating-User') {
                   steps {
                       dir('USER') {  git branch: 'main', url: 'https://github.com/codesud/user.git'
                          sh '''
                             echo user
                          '''
                            }
                        }
                   }
               stage('Creating-Catalogue') {
                   steps {
                       dir('Catalogue') {  git branch: 'main', url: 'https://github.com/codesud/catalogue.git'
                          sh '''
                             echo catalogue 
                          '''
                            }
                        }
                  }
            stage('Creating-Payment') {
                steps {
                    dir('PAYMENT') {  git branch: 'main', url: 'https://github.com/codesud/payment.git'
                          sh '''
                                echo payment
                          '''
                         }
                     }
                }
             } // Parallel Stages Completed
          }   // Stage Completed
         stage('Backend-2') {
            parallel {
            stage('Creating-Cart') {
                steps {
                    dir('CART') {  git branch: 'main', url: 'https://github.com/codesud/cart.git'
                          sh '''
                            echo cart
                          '''
                         }
                     }
                }
            stage('Creating-Shipping') {
                steps {
                    dir('SHIPPING') {  git branch: 'main', url: 'https://github.com/codesud/shipping.git'
                          sh '''
                            echo shipping
                          '''
                         }
                     }
                  }
              } // Parallel Stages Completed
           }   // Stage Completed
                   stage('Creating-Frontend') {
                       steps {
                           dir('FRONTEND') {  git branch: 'main', url: 'https://github.com/codesud/frontend.git'
                              sh '''
                                    echo frontend
                              '''
                                }
                            }
                       }
                  }
            }