pipeline {
    agent any
    stages{
        stage('Build') {
            steps {
                sh '/Users/vincentyoung/Git/Jenkins/apache-maven-3.5.4/bin/mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage('Deploy to Staging'){
            steps {
                build job: 'deploy-to-staging'
            }
        }
        stage('Deploy to Production'){
            steps {
                timeout(time:5, unit:'DAYS') {
                    input message:'Approve Production Deployment?'
                }
                build job:'deploy-to-prod'
            }
            post{
                success{
                    echo 'Code deployed to Production.'
                }
                failure {
                    echo 'Deployment failed.'
                }
            }
        }
    }
}