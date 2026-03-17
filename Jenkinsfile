pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "gaurisathya/gauri-bcs34-cicd"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git 'https://github.com/GauriLekshmiSathya/ci-cd-test.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Login to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials',
                usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                }
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker push $DOCKER_IMAGE'
            }
        }

    }
}