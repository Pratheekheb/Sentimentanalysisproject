pipeline {
    agent any

    environment {
        IMAGE_NAME = 'sentiment-analysis-image'
        CONTAINER_NAME = 'sentiment-analysis-container'
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
                    // Create a Dockerfile
                    writeFile file: 'Dockerfile', text: '''
                    FROM python:3.9-slim

                    WORKDIR /app

                    COPY requirements.txt .
                    RUN pip install --no-cache-dir -r requirements.txt

                    COPY . .

                    CMD ["python", "model.py"]
                    '''
                    // Build the Docker image
                    sh "docker build -t ${IMAGE_NAME} ."
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Run the Docker container
                    sh "docker run --name ${CONTAINER_NAME} --rm ${IMAGE_NAME}"
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
