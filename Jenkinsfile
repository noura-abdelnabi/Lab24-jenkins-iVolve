
@Library('SahredLibrary-NTI') _ 

pipeline {
    agent { label 'shared-lib' } 

    stages {
        stage('Build') {
            steps {
                buildApp() 
            }
        }
        stage('Docker Build & Push') {
            steps {
                buildAndPushImage("noura/my-app:${env.BRANCH_NAME}", "docker-hub-creds")
            }
        }
        stage('Deploy') {
            steps {
                script {
                    deployToK8s("noura/my-app:${env.BRANCH_NAME}", "deployment.yaml", "k8s-token", "k8s-api")
                }
            }
        }
    }
}
