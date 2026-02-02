pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
                git 'https://github.com/23MH1A05S5/jenkinss.git'
            }
        }

        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Stop & Remove Old Container') {
            steps {
                sh '''
                docker stop harshi || true
                docker rm harshi || true
                '''
            }
        }

        stage('Remove Old Image') {
            steps {
                sh '''
                docker rmi cont || true
                '''
            }
        }

        stage('Docker Image Build') {
            steps {
                sh 'docker build -t cont .'
            }
        }

        stage('Docker Deploy') {
            steps {
                sh 'docker run -d -p 8081:8080 --name harshi cont'
            }
        }
    }
}
