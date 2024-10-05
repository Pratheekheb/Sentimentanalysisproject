pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
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
                        bat 'venv\\Scripts\\activate.bat'
                        bat 'venv\\Scripts\\pip install -r requirements.txt'
                    }
                }
            }
        }

        stage('Run Script') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'python3 model.py' // replace with your actual script
                    } else {
                        bat 'python model.py' // replace with your actual script
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
