pipeline {
    agent any

    environment {
        DEPLOY_DIR = "/var/www/html"
        REPO_URL = "https://github.com/mounikamandragutti/Car-website.git"
        BRANCH = "main"
    }

    stages {

        stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }

        stage('Checkout Code') {
            steps {
                git branch: "${BRANCH}", url: "${REPO_URL}"
            }
        }

        stage('Verify Files') {
            steps {
                sh 'ls -la'
            }
        }

        stage('Deploy to Apache') {
            steps {
                sh '''
                echo "Deploying website to Apache directory..."
                sudo rm -rf ${DEPLOY_DIR}/*
                sudo cp -r * ${DEPLOY_DIR}/
                '''
            }
        }

        stage('Restart Apache') {
            steps {
                sh 'sudo systemctl restart apache2'
            }
        }
    }

    post {
        success {
            echo "Deployment Successful!"
        }
        failure {
            echo "Deployment Failed!"
        }
    }
}
