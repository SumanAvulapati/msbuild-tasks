pipeline{
    agent any
    
    environment {
        dotnet ='/usr/bin/dotnet'
        }
        
    triggers {
        pollSCM 'H * * * *'
    }
    stages{
        stage ('Clean workspace') {
            steps {
                cleanWs()
            }
        }        
        stage('Checkout') {
            steps {
                checkout scm
                }
        }
        stage('Nuget Restore, Build & Run') {
            steps {
                sh './build.sh'
            }
        }        
    }
    post{
        always{
            emailext body: "${currentBuild.currentResult}: Job   ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}",
            recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']],
            subject: "Jenkins Build ${currentBuild.currentResult}: Job ${env.JOB_NAME}"
        }
    }    
 }        