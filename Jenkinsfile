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
                withDockerRegistry([ credentialsId: '47864573-370a-49ec-b1a4-6cf0b395d7c9', url: '' ]) {
                    sh 'docker push $IMAGE_NAME'
                }
            }
        }
    }
}
