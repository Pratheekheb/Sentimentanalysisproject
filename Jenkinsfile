pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/thegrandaviator/Project-3-EXL-Training-Batch1'
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
                        sh 'python app.py'
                    } else {
                        bat 'python app.py'
                    }
                }
            }
        }

        // stage('Deploy to GitHub') {
        //     steps {
        //         script {
        //             sh 'git config user.email "you@example.com"'
        //             sh 'git config user.name "Your Name"'
        //             sh 'git add .'
        //             sh 'git commit -m "Automated commit from Jenkins"'
        //             sh 'git push origin ${GIT_BRANCH}'
        //         }
        //     }
        // }
    }

    post {
        always {
            cleanWs()
        }
    }
}
