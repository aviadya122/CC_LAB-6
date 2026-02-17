pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                echo 'Repository cloned automatically by Jenkins'
            }
        }

        stage('Build Backend Image') {
            steps {
                sh '''
                docker build -t backend-app backend
                '''
            }
        }

        stage('Run Backend Containers') {
            steps {
                sh '''
                docker rm -f backend1 backend2 || true
                docker run -d --name backend1 backend-app
                docker run -d --name backend2 backend-app
                '''
            }
        }

        stage('Run Nginx') {
            steps {
                sh '''
                docker rm -f nginx || true
                docker build -t nginx-lb nginx
                docker run -d -p 80:80 --name nginx nginx-lb
                '''
            }
        }
    }
}
