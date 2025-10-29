pipeline {
    agent any 
    stages {
        stage('Build Docker Image'){
            steps{
                bat "docker build -t registration:v1"
            }
        }
        stage('Run docker container'){
            steps{
                bat "docker rm -f registration container" || exit 0
                bat "docker run -t -name registration:v1"
            }
        }
        stage('Deploy to Kubernetes'){
            steps{
                bat 'kubectl apply -f deployment.yaml --validate=false'
                bat 'kubectl apply -f service.yaml'
            }
        }
        post{
            success{
                echo 'pipeline completed successfully'
            }
            failure{
                echo 'pipeline failed please check the logs'
            }
        }
    }
}
