pipeline {
    agent any
    environment {
        AWS_ACCESS_KEY_ID = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
    }
    stages {
        stage('clone') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], 
                    extensions: [], 
                    userRemoteConfigs: [[
                        url: 'git@github.com:polimerakalyan/create-ec2.git', 
                        credentialsId: 'your-ssh-credential-id'
                    ]])
            }
        }
        stage('init') {
            steps {
                sh 'terraform init'
            }
        }
        stage('validate') {
            steps {
                sh 'terraform validate'
            }
        }
        stage('plan') {
            steps {
                sh 'terraform plan'
            }
        }
        stage('apply') {
            steps {
                sh 'terraform apply -auto-approve'
            }
        }
    }
}
