pipeline {
    agent any

    environment {
        DOCKER_HUB_CREDENTIALS = credentials('dockerHubCred')
        IMAGE_NAME = "nitishkashyap08/react-app"
        IMAGE_TAG = "latest"
    }

    stages {
        stage('Clone') {
            steps {
                checkout scm
            }
        }

        stage('Build Only') {
            agent {
                docker {
                    image 'node:18-alpine'
                    args '-u root:root'
                }
            }
            steps {
                sh 'npm install'
                sh 'npm run build'
                // Tests are skipped
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
            echo 'Build and push successful!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
