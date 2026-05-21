pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh '"%PYTHON%" -m venv venv'
                sh 'venv\\Scripts\\pip install -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                sh 'venv\\Scripts\\pytest'
            }
        }

        stage('Deploy') {
            steps {
                sh 'start /B venv\\Scripts\\python app.py'
            }
        }
    }
}
