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
                sh '''
                    python3 -m venv venv
                    . venv/bin/activate
                    pip install -r requirements.txt
                '''
            }
        }
        stage('Test') {
            steps {
                sh '''
                    . venv/bin/activate
                    pytest
                '''
            }
        }
        stage('Deploy') {
    steps {
        sh '''
            . venv/bin/activate
            fuser -k 5000/tcp || true
            nohup python3 app.py > /var/jenkins_home/flask.log 2>&1 &
            sleep 2
            curl http://localhost:5000
        '''
    }
}
    }
}
