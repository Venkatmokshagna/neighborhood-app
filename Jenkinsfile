pipeline {
    agent any

    environment {
        IMAGE_NAME = "venkatmokshagna/neighborhood-app"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/Venkatmokshagna/neighborhood-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Run Unit Tests') {
            steps {
                sh 'docker run --rm $IMAGE_NAME python3 -m unittest discover tests'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withDockerRegistry([ credentialsId: 'dockerhub-creds', url: '' ]) {
                    sh 'docker push $IMAGE_NAME'
                }
            }
        }
    }
}
