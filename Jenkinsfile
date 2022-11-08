 node {
        stage('SCM Checkout')
        {
            git credentialsId: 'ab85cc4b-c108-44bb-a33b-4e415592a692', url: 'https://github.com/balti09/php_ecommerce_app.git'
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
