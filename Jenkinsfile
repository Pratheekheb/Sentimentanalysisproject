pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    def image = docker.build("sentiment-analysis:latest")
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Run the Docker container
                    docker.image("sentiment-analysis:latest").inside {
                        // The container will run the CMD specified in the Dockerfile
                        sh 'python model.py'  // This line may be optional based on CMD in Dockerfile
                    }
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
