pipeline {
    agent any

    environment {
        DOCKER_HUB_CREDENTIALS = credentials('dockerHubCred') // Your Jenkins Docker Hub credentials ID
        IMAGE_NAME = "nitishkashyap08/react-app"
        IMAGE_TAG = "latest"
    }

    stages {
        stage('Clone') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test -- --watchAll=false'
            }
        }

        stage('Docker Build & Push') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerHubCred') {
                        def appImage = docker.build("${IMAGE_NAME}:${IMAGE_TAG}")
                        appImage.push()
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
        success {
            echo 'Build, test, and push successful!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
