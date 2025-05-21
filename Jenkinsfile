pipeline {
    agent any

    tools {
        nodejs 'mynodejs'
    }

    environment {
        DOCKER_NAME = 'nitishkashyap08'
    }

    stages {
        stage('Clone') {
            steps {
                git url: 'https://github.com/Nitishkashyap08/ReactJs-Frontend-CICD.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ${DOCKER_NAME}/my-app:latest .'
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'DockerCredId', usernameVariable: 'DOCKER_NAME', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'sudo docker build -t ${DOCKER_NAME}/my-app:latest .'
                 sh 'echo $DOCKER_PASS | sudo docker login -u $DOCKER_NAME --password-stdin'
                 sh 'sudo docker push $DOCKER_NAME/my-app:latest'

                }
            }
        }
    }
}
