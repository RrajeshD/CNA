#!groovy

def err
def status = 'sucess'

pipeline {
   agent any
   stages {
      stage('Clone Repo') {
          steps {
              script {
              // Get some code from a GitHub repository
              git branch: 'main',

              credentialsId: 'Terraform-Integration',

              url: "https://github.com/RrajeshD/CNA-Infra.git" 'HEAD-main'

              }
          }
      }
        stage ('Converting to TF files') {
          steps {
            script {
            sh'''
            mv mainfile.txt main.tf
            mv variablefile.txt variables.tf
            '''
            }
        }
        }
    stage ('Terraform-init') {
        steps {
            script {
                sh'''
                terraform init
                '''
            }
        }
    }
    stage ('Terraform-Plan') {
        steps {
            script {
                sh '''
                terraform plan
                '''
            }
            }
        }
    stage ('Terraform Apply') {
        steps {
            script {
                sh '''
                #terraform apply --auto-approve
                '''
            }
        }
    }
    }
}
