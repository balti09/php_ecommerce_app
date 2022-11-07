 node {
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
