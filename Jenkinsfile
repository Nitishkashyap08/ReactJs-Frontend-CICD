pipeline{
    agent any
    tools{
        maven 'mymaven'
    }
    stages{
        stage('clone'){
            steps{
                git url : "https://github.com/Nitishkashyap08/ReactJs-Frontend-CICD.git" ,branch : "main"
            }
        }
        stage('build'){
            steps{
            sh 'npm build'
            sh 'npm install'
            }
        }
        stage('test'){
            steps{
                sh 'npm test'
            }
        }
    }
}
