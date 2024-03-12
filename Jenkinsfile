pipeline {
    agent any
    
    stages {
        stage('Checkout from Git'){
            steps{
                git branch: 'main', url: 'https://github.com/safuvanh/Netflix_clone'
            }
        }
        
        stage("Docker Build & Push"){
            steps{
                script{
                   withDockerRegistry(credentialsId: 'docker', toolName: 'docker'){   
                       sh "docker build --build-arg TMDB_V3_API_KEY=<************> -t netflix ."
                       sh "docker tag netflix safuvanh/netflix:latest "
                       sh "docker push safuvanh/netflix:latest "
                    }
                }
            }
        }
        
        stage('Deploy to container'){
            steps{
                sh 'docker run -d -p 8080:80 safuvanh/netflix:latest'
            }
        }
    }
}
