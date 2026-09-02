brary('my-shared-library') _

pipeline {
    agent any

    environment {
        APP_NAME = 'docker-app-demo'
        DOCKERHUB_USER = 'lizaaliza'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building Docker Image...'
                script {
                    myLibrary.buildApp()
                }
            }
        }

        stage('Test') {
            steps {
                echo 'Testing...'
                script {
                    myLibrary.test()
                }
                sh 'echo "Tests passed successfully"'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying to Docker Hub...'
                script {
                    myLibrary.deployApp()
                }
            }
        }
    }
}
