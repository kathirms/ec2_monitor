pipeline {
    agent any
    stages {
    
        
        stage ('Creating EC2 Instance State Change Alert') {
            steps {
                script {
                    try {
                         
                        sh '''#!/bin/bash
                            cd /var/lib/jenkins/workspace/Mydemo
                            sed -i -e "s|us-east-1|${AWS_REGION}|g" -e "s|{account-name}|${AWS_PROFILE}|g" main.tf
                            sudo terraform init
                            sudo terraform plan
                            sudo terraform apply -var provider_profile=${AWS_PROFILE} -auto-approve -lock=false
                            
                            '''
                    }

                    catch (Exception err) {
                        currentBuild.result = 'FAILED'
                        sh '''#!/bin/bash
                               echo "cant deploy ec2 instance state change alert"
                               exit 1
                               '''
                    }
                }
            }
            
        }
      
    }
    
}    
