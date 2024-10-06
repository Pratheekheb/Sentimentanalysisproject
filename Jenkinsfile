pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/yourusername/yourrepository.git'
        GIT_BRANCH = 'main'
        GIT_CREDENTIALS_ID = 'your-git-credentials-id'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: "${GIT_BRANCH}", url: "${GIT_REPO}", credentialsId: "${GIT_CREDENTIALS_ID}"
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'python3 -m venv venv'
                        sh '. venv/bin/activate'
                        sh 'pip install -r requirements.txt'
                    } else {
                        bat 'python -m venv venv'
                        bat 'venv\\Scripts\\activate'
                        bat 'pip install -r requirements.txt'
                    }
                }
            }
        }

        stage('Run Script') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'python model.py'
                    } else {
                        bat 'python model.py'
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
