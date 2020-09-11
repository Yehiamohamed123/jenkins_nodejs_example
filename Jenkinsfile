 pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'docker build -f dockerfile . -t yehiam/jenkins_node:v1.0'
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
                sh 'docker run -d -p 4000:4000 yehiam/jenkins_node:v1.0'
            }
        }
    }
 }
