pipeline {
    agent any

    environment {
        DEV_REPO = kaviyarasuparthiban/react-app-dev
        PROD_REPO = kaviyarasuparthiban/react-app-prod
    }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t react-app .'
            }
        }

        stage('Push Image to DockerHub') {
            steps {
                script {
                    if (env.BRANCH_NAME == 'dev') {
                        sh """
                        docker tag react-app $DEV_REPO:latest
                        docker push $DEV_REPO:latest
                        """
                    } else if (env.BRANCH_NAME == 'master') {
                        sh """
                        docker tag react-app $PROD_REPO:latest
                        docker push $PROD_REPO:latest
                        """
                    }
                }
            }
        }
    }
}

