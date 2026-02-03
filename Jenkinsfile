pipeline {
    agent any

    triggers {
        cron('H/5 * * * *')   // runs every minute
    }

    environment {
        DOCKERHUB_CRED = credentials('dockerhub')
        IMAGE_NAME = "vanireddy2025/my_mavenapp"
    }

    stages {

        stage('Checkout') {
            steps {
                git url: 'https://github.com/Vani-prog/my_mavenapp.git',
                    branch: 'main'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("${IMAGE_NAME}:latest")
                }
            }
        }

        stage('Push Image to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub') {
                        dockerImage.push('latest')
                    }
                }
            }
        }
    }
}
