pipeline{
    agent { label 'amit'}
    
    stages{
       stage("Code") {
            steps {
                echo "GitHub source code checked out successfully"
            }
        }
        stage("Build") {
                steps {
                    echo "Building Docker image"
            
                    sh 'docker build -t notes-app:latest .'
                }
            }
 
        stage("Push to Docker Hub") {
            steps {
                echo "Pushing image to Docker Hub"
        
                withCredentials([usernamePassword(
                    credentialsId: "dockerHubCred",
                    usernameVariable: "dockerHubUser",
                    passwordVariable: "dockerHubPass"
                )]) {
                    sh '''
                        echo "$dockerHubPass" | docker login -u "$dockerHubUser" --password-stdin
        
                        docker tag notes-app:latest "$dockerHubUser/notes-app:latest"
        
                        docker push "$dockerHubUser/notes-app:latest"
                    '''
                }
            }
        }

       
        stage("Deploy") {
            steps {
                echo "Deploying application using Docker Compose"
        
                sh '''
                    docker compose pull django_app
                    docker compose up -d
                '''

                echo "Successful application deployed."
            }
        }      
    }
}
