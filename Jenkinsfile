pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building application...'
                sh 'python3 -m py_compile app/app.py'
                echo 'Build completed successfully.'
            }
        }

        stage('Test') {
            steps {
                echo 'Creating Python virtual environment...'
                sh 'python3 -m venv .venv'

                echo 'Installing dependencies...'
                sh '.venv/bin/pip install -r requirements.txt'

                echo 'Running tests...'
                sh '.venv/bin/pytest tests/'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }

        failure {
            echo 'Pipeline failed. Check the build logs.'
        }
    }
}
