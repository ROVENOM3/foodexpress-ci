pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                bat 'python -m venv venv'
                bat 'venv\\Scripts\\python -m pip install pytest flake8'
            }
        }

        stage('Code Quality') {
            steps {
                bat 'venv\\Scripts\\python -m flake8 cart.py orders.py || exit /b 0'
            }
        }

        stage('Test') {
            steps {
                bat 'venv\\Scripts\\python -m pytest'
            }
        }

        stage('Package') {
            steps {
                bat 'venv\\Scripts\\python package.py'
                archiveArtifacts artifacts: 'foodexpress.zip', fingerprint: true
            }
        }
    }

    post {
        success {
            echo 'SUCCESS: all stages passed and the artifact was created.'
        }

        failure {
            echo 'FAILURE: one stage failed. Open the red stage to see why.'
        }
    }
}