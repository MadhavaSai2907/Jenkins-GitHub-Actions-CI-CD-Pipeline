pipeline {
    agent any

    environment {
        APP_DIR = "flask-app"
    }

    stages {

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
                nohup python3 app.py &
                '''
            }
        }
    }

    post {
        success {
            mail to: 'hanusaimadhava@gmail.com',
                 subject: "SUCCESS: Jenkins Pipeline",
                 body: "Build and deployment successful."
        }
        failure {
            mail to: 'hanusaimadhava@gmail.com',
                 subject: "FAILED: Jenkins Pipeline",
                 body: "Build failed. Check Jenkins logs."
        }
    }
}
