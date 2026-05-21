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
                    pkill -f "python3 app.py" || true
                    JENKINS_NODE_COOKIE=dontKillMe nohup python3 app.py > /var/jenkins_home/flask.log 2>&1 &
                    sleep 3
                    curl http://localhost:5000
                '''
            }
        }
    }
}
