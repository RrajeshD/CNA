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

              credentialsId: 'Github-Intigration',

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
            sed -i "s/why/$access_key/g" main.tf
            sed -i "s/not/$secret_key/g" main.tf
            cat main.tf -n
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
                terraform apply --auto-approve
                '''
            }
        }
    }
    }
}
