 pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'docker build -f dockerfile . -t yehiam/jenkins_node:v1.0'
            }
        }
               post{
             success{
              slackSend(color:'#00FF00',message:'successful':job '${env.JOB_NAME}${env.BUILD_NUMBER}')
            }
             failure{
                slackSend(color:'#FF0000',message:'failure')
            }
             aborted{
                slackSend(color:'#FFFF00',message:'aborted')
            }
            
            }
    }
        stage('Push') {
            steps {
                withCredentials([usernamePassword(credentialsId:"docker",usernameVariable:"USERNAME",passwordVariable:"PASSWORD")]){
             
                
                sh 'docker login --username $USERNAME --password $PASSWORD'
                sh 'docker push  yehiam/jenkins_node:v1.0'
            }
           
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker run -d -p 5000:3000 yehiam/jenkins_node:v1.0'
            }
        }
    }
 }
