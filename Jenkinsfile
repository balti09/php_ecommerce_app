pipeline{

	    agent any

      
        stages{
            stage('SCM Checkout')
            { 
                steps{
                    git branch: 'main' , credentialsId: 'ed6b6f25-0a70-4023-aed9-b7e4a4882af5', url: 'https://github.com/balti09/php_ecommerce_app.git'
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
                            //bat 'docker push balti99/e-commerce_app/php_ecommerce_pipeline_web:latest'
                           bat 'docker push balti99/e-commerce_app/mysql:latest'
                    }
                }
                
            }
        stage('PUSH image to Docker Hub')
            {
                steps{
                    bat 'echo ff'
                   // bat 'docker tag mysql:latest balti99/e-commerce_app/mysql:latest'
                   // bat 'docker tag php_ecommerce_pipeline_web:latest balti99/e-commerce_app/php_ecommerce_pipeline_web:latest'
                    //bat 'docker push balti99/e-commerce_app/php_ecommerce_pipeline_web:latest'
                    //bat 'docker push balti99/e-commerce_app/mysql:latest'
                }
                
            }
        }    
}
