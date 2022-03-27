pipeline {
    agent any

    stages {
        stage('SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/SiriveruJagadeesh/server-2.git/mai'
            }
        }
       
        stage('Build Docker Image') {
            steps {
                script {
                    
                 sh 'docker build -t jagadeeshsiriveru/webimg:v1 .'
                }
            }
        }
        stage('Pushing Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'e61a8d5e-2543-4b62-88e7-9445c1052dbb', toolName: 'DOCKER') {
               sh 'docker push jagadeeshsiriveru/webimg:v1'
               
                }
              }
            }
          }
        
        stage('Run Container on EC2-INSTANCE'){
            steps {
                sshagent(['EC2-INSTANCE']) {
                sh "ssh -o StrictHostKeyChecking=no ec2-user@13.127.194.123 'docker run -p 4000:4000 -d jagadeeshsiriveru/webimg:v1'"
                }
                
                sshagent(['EC2-INSTANCE']) {
                sh "ssh -o StrictHostKeyChecking=no ec2-user@3.108.52.200 'docker run -p 4000:4000 -d jagadeeshsiriveru/webimg:v1'"
                  }
            }
        }
    }
}
