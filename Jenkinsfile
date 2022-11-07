pipeline {
    agent any

    stages {
        stage('SCM Checkout')
        {
            url: 'https://github.com/balti09/php_ecommerce_app.git'
        }
        
        stage('Run Docker Compose File')
        {
            sh 'docker-compose build'
            sh 'docker-compose up -d'
        }
        stage('PUSH image to Docker Hub')
        {
            withCredentials([ credentialsId: "DockerHubPW" ,  url: ""]) 
            {
               dockerImage.push()
            }
            
        }
    }
}