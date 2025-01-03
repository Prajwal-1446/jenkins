pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "python-flask-app"
        DOCKER_REGISTRY = "prajwal351" // Replace with your Docker Hub or private registry
    }
    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/Prajwal-1446/jenkins'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ${DOCKER_IMAGE} .'
            }
        }
        stage('Push Docker Image') {
            steps {
                sh 'docker tag ${DOCKER_IMAGE} ${DOCKER_REGISTRY}/${DOCKER_IMAGE}'
                sh 'docker push ${DOCKER_REGISTRY}/${DOCKER_IMAGE}'
            }
        }
        stage('Deploy Application') {
            steps {
                sh 'docker run -d -p 5000:5000 ${DOCKER_IMAGE}'
            }
        }
    }
    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}
