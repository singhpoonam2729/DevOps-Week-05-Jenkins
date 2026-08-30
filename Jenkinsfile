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
                python3 -m py_compile app/app.py
                echo 'Build completed successfully.'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                python3 -m pytest tests/
                echo 'All tests passed successfully.'
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

