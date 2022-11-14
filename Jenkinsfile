pipeline{

	    agent any

      
        stages{
            stage('SCM Checkout')
            { 
                steps{
                    git branch: 'main' , credentialsId: 'ed6b6f25-0a70-4023-aed9-b7e4a4882af5', url: 'https://github.com/balti09/php_ecommerce_app.git'
                }
            
            }
            stage('SonarQube analysis') {
                tools {
                    jdk "java" // the name you have given the JDK installation in Global Tool Configuration
                }
                environment {
                    scannerHome = tool 'sonar' // the name you have given the Sonar Scanner (in Global Tool Configuration)
                }
                steps{
                    
                    withSonarQubeEnv('php-ecommerce') { // If you have configured more than one global server connection, you can specify its name
                    bat "cd ${scannerHome}"
                    bat 'sonar-scanner.bat'
                }
                }
                
            }
            stage('Run Docker Compose File')
            {
                steps{
                    bat 'docker-compose build'
                    bat 'docker-compose up -d'
                }
            }
            stage('Docker login')
            {
                steps{
                    withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'docker_pass', usernameVariable: 'docker_user')]) {
                          
                          
                          bat 'docker login -u %docker_user% -p %docker_pass%'
                           
                    }
                }
                
            }
        stage('PUSH image to Docker Hub')
            {
                steps{
                  
                    bat 'docker tag mysql:latest balti99/e-commerce_app:V1'
                    bat 'docker tag php_ecommerce_pipeline_web:latest balti99/e-commerce_app:V2'
                    bat 'docker push balti99/e-commerce_app:V1'
                    bat 'docker push balti99/e-commerce_app:V2'
                }
                
            }
        }    
}
