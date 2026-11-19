@Library("Shared") _
pipeline{
    agent { label 'amit'}
    
    stages{
       stage("Code") {
            steps {
                echo "this is coding phase"
                script{
                    hello()
                }
            }
        }
        stage("Build") {
                steps {
                   script{
                       docker_build("notes-app","latest","admin2219")
                }
            }
        }
 
        stage("Push to Docker Hub") {
            steps {
               script{
                   docker_push("notes-app","latest","admin2219")
               }
            }
        }
        
        stage("Deploy") {
            steps {
                echo "Deploying application using Docker Compose"
                    script{
                        docker_compose()
                }
            }
        }      
    }
}
