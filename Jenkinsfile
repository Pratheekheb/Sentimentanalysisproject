pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/Pratheekheb/Sentimentanalysisproject.git'
        GIT_BRANCH = 'main'
        GIT_CREDENTIALS_ID = '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'  // Update this to the ID of your Jenkins-stored GitHub token credentials
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
                            python3 -m venv venv
                            . venv/bin/activate
                            pip install -r requirements.txt
                        '''
                    } else {
                        bat '''
                            python -m venv venv
                            venv\\Scripts\\activate
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
                            . venv/bin/activate
                            python model.py
                        '''
                    } else {
                        bat '''
                            venv\\Scripts\\activate
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
