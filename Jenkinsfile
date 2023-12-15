    pipeline {
        agent any
        stages {
            stage('Create ECR Repo') {
                steps{
                    build job: 'create-ecr-repo'
                }
            }
            stage('Build and Push Images'){
                steps{
                    build job: 'build-and-push-images-to-ecr'
                }            
            }
            stage('Deploy to Cluster'){
                steps{
                    build job: 'deploy-the-app'
                }            
            }
            stage('Delete the Deployment'){
                steps{
                    timeout(time:5, unit:'DAYS'){
                        input message:'Approve to DELETE Deployment?'
                    }
                    build job: 'delete-the-app'
                }
            }
        }
    }