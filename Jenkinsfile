pipeline {
    agent any 
    options {
        ansiColor('xterm')
    }
    parameters {
        choice(name: 'ENV', choices: ['dev', 'prod'], description: 'Select Your Envirovment')
        //choice(name: 'ACTION', choices: ['apply', 'destroy'], description: 'Select Your Action')
    }
    stages {
        stage('Terraform Init') {
            steps {
                sh "terrafile -f env-${ENV}/Terrafile"
                sh "terraform init -backend-config=env-${ENV}/${ENV}-backend.tfvars"
            }
        }
        stage('Terraform Plan') {
            steps {
                sh "terraform plan -var-file=env-${ENV}/${ENV}.tfvars"
            }
        }
        stage('Terraform apply') {
            steps {
                sh "terraform apply -auto-approve -var-file=env-${ENV}/${ENV}.tfvars"
            }
        }
        // stage('Terraform Action') {
        //     steps {
        //         sh "terraform ${ACTION} -auto-approve -var-file=env-${ENV}/${ENV}.tfvars"
        //     }
        // }
    }
}