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
                    def image = docker.build('your-docker-image-name')
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Run the Docker container and execute model.py
                    docker.image('your-docker-image-name').inside {
                        // Use 'python' to execute model.py
                        bat 'python model.py' // Use 'bat' for Windows
                        // For Linux, you would use 'sh' instead of 'bat'
                    }
                }
            }
        }
    }

    post {
        always {
            cleanWs() // Clean workspace after build
        }
    }
}
