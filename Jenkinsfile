 node {
        stage('SCM Checkout')
        {
            git branch: 'main' , credentialsId: 'ed6b6f25-0a70-4023-aed9-b7e4a4882af5', url: 'https://github.com/balti09/php_ecommerce_app.git'
        }
        stage('Run Docker Compose File')
        {
            bat 'docker-compose build'
            bat 'docker-compose up -d'
        }
        stage('PUSH image to Docker Hub')
        {
            withCredentials([ credentialsId: "DockerHubPW" ,  url: ""]) 
            {
               dockerImage.push()
            }
            
        }
    }
