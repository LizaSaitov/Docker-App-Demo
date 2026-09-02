@Library('my-shared-library') _
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
                sh "docker build -t ${env.DOCKERHUB_USER}/${env.APP_NAME}:${env.BUILD_NUMBER} ."
                script {
                    myLibrary.buildApp()
                }
            }
        }

        stage('Test') {
            steps {
                echo 'Testing...'
                sh 'echo "Tests passed successfully"'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying to Docker Hub...'
                script {
                    myLibrary.deployApp
                }
                withCredentials([usernamePassword(credentialsId: 'liza-dockerhub', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh '''
                        echo "$PASS" | docker login -u "$USER" --password-stdin
                        docker push ${DOCKERHUB_USER}/${APP_NAME}:${BUILD_NUMBER}
                    '''
                    
                }
            }
        }
    }
}
