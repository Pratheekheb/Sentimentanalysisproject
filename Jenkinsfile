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
                        sh '''
                            conda create -n sentiment_env python=3.8 -y
                            source activate sentiment_env
                            pip install -r requirements.txt
                        '''
                    } else {
                        bat '''
                            conda create -n sentiment_env python=3.8 -y
                            conda activate sentiment_env
                            pip install -r requirements.txt
                        '''
                    }
                }
            }
        }

        stage('Run Script') {
            steps {
                script {
                    if (isUnix()) {
                        sh '''
                            source activate sentiment_env
                            python model.py
                        '''
                    } else {
                        bat '''
                            conda activate sentiment_env
                            python model.py
                        '''
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
