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
                build job: 'Deploy-to-staging'
            }
        }
    }
}