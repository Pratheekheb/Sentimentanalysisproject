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
                        sh 'source venv/bin/activate && pip install -r requirements.txt'
                    } else {
                        bat 'python -m venv venv'
                        bat 'call venv\\Scripts\\activate && pip install -r requirements.txt'
                    }
                }
            }
        }

        stage('Run Script') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'python app.py'
                    } else {
                        bat 'python app.py'
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
