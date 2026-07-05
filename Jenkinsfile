pipeline {
    agent any

    environment {
        APP_NAME = "FlaskApp"
    }

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/abhishekshukla831-cmyk/flask_Practice'
            }
        }

        stage('Build') {
            steps {
                sh '''
                python3 -m venv venv
                . venv/bin/activate
                pip install --upgrade pip
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
                echo "Deploying application..."
                pkill -f app.py || true
                nohup python app.py > app.log 2>&1 &
                '''
            }
        }
    }

    post {

        success {
            emailext(
                subject: "SUCCESS: Jenkins Build",
                body: "Pipeline completed successfully.",
                to: "abhishek.shukla831@gmail.com"
            )
        }

        failure {
            emailext(
                subject: "FAILED: Jenkins Build",
                body: "Pipeline Failed.",
                to: "abhishek.shukla831@gmail.com"
            )
        }
    }
}