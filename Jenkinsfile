pipeline {
    agent any

    environment {
        Container_name = "nestjs-app"
        Image_name = "nestjs-img"
        Email = "abdulmoiz95972@gmail.com"
        Port = "3000"
    }

    stages {
        stage('Clone Code') {
            steps {
                git url: "https://github.com/AbdulM0izz/nestjs-ci-cd.git", branch: "main"
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $Image_name .'
            }
        }

        stage('Remove Previous Container') {
            steps {
                sh '''
                docker stop $Container_name || true
                docker rm $Container_name || true
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                docker run -d -p ${Port}:${Port} --name $Container_name $Image_name
                '''
            }
        }

        stage('Send Email') {
            steps {
                emailext (
                    subject: "NestJS App Deployed",
                    body: "The application has been deployed successfully at http://13.53.76.95:${Port}/",
                    to: "${Email}"
                )
            }
        }
    }
}
