pipeline {
    agent {
        // Specify the Docker agent label
        docker {
            image 'python:3.9' // Replace with your desired base image
            label 'docker' // The label of the agent that has Docker installed
        }
    }

    environment {
        DOCKER_CREDENTIALS_ID = 'manjunath.chavan2017@gmail.com' // Set this to your Docker registry credentials ID
        DOCKER_IMAGE = 'Python-Eduflix' // Set the desired image name
        DOCKER_REGISTRY_URL = 'https://index.docker.io/v1/' // Replace with your Docker registry URL
    }

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
                    def image = docker.build("${DOCKER_IMAGE}", "-f Dockerfile .")
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Run the Docker container and execute model.py
                    docker.image("${DOCKER_IMAGE}").inside {
                        sh 'python model.py' // Use 'sh' for Unix-based systems
                        // bat 'python model.py' // Use this for Windows
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
