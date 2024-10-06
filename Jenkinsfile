pipeline {
    agent any
    stages {
        stage('Checkout SCM') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], 
                    userRemoteConfigs: [[url: 'https://github.com/Pratheekheb/Sentimentanalysisproject.git', credentialsId: '5f06b98e-537d-4c25-bef5-be1a4bfd66ac']]])
            }
        }
        stage('Install Dependencies') {
            steps {
                script {
                    // Create and set up the Conda environment
                    bat 'conda create -n sentiment_env python=3.8 -y'
                }
            }
        }
        stage('Activate Environment') {
            steps {
                script {
                    // Activate the environment
                    bat 'conda activate sentiment_env'
                }
            }
        }
        stage('Install Required Packages') {
            steps {
                script {
                    // Install the required dependencies from requirements.txt (if applicable)
                    bat 'conda activate sentiment_env && pip install -r requirements.txt'
                }
            }
        }
        stage('Run Sentiment Analysis Model') {
            steps {
                script {
                    // Run the model.py script within the activated conda environment
                    bat 'conda activate sentiment_env && python model.py'
                }
            }
        }
    }
    post {
        always {
            // Clean up the workspace after the build
            cleanWs()
        }
    }
}
