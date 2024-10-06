pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/Pratheekheb/Sentimentanalysisproject.git'
        GIT_BRANCH = 'main'
        GIT_CREDENTIALS_ID = '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'
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
