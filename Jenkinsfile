pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code from GitHub...'
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
                sh '.venv/bin/python -m pip install -r requirements.txt'

                echo 'Running automated tests...'
                sh '.venv/bin/python -m pytest tests/'
            }
        }

        stage('Validation') {
            steps {
                echo 'Running additional validation...'
                sh 'test -f app/app.py'
                sh 'test -f tests/test_app.py'
                sh 'test -f requirements.txt'
                sh 'test -f Jenkinsfile'
                echo 'All required project files are present.'
            }
        }
    }

    post {
        success {
            echo 'CI Pipeline completed successfully!'
        }

        failure {
            echo 'CI Pipeline failed. Check the Console Output.'
        }
    }
}

