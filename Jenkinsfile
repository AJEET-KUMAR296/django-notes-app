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
        stage("Push to DockerHub"){
            steps{
                dockerpush("dockerHubCreds","notes-app","latest")
            }
        }
        stage("Deploy"){
            steps{
                deploy()
            }
        }
        
    }
}
