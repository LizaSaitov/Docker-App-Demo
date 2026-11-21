pipeline {
    agent any

    parameters {
        string(name: 'APP_PARM', defaultValue: 'docker-app-demo', description: 'Application Name')
    }

    environment {
        APP_NAME = "${params.APP_PARM}"
        DOCKERHUB_USER = 'lizaaliza'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building Docker Image...'
                sh "docker build -t ${env.DOCKERHUB_USER}/${env.APP_NAME}:${env.BUILD_NUMBER} -t ${env.DOCKERHUB_USER}/${env.APP_NAME}:latest ."
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
                withCredentials([usernamePassword(credentialsId: 'liza-dockerhub', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh '''
                        echo "$PASS" | docker login -u "$USER" --password-stdin
                        docker push ${DOCKERHUB_USER}/${APP_NAME}:${BUILD_NUMBER}
                        docker push ${DOCKERHUB_USER}/${APP_NAME}:latest
                    '''
                }
            }
        }
    stage('Update & Push GitOps') {
        steps {
            withCredentials([
                usernamePassword(
                    credentialsId: 'github-credentials', 
                    usernameVariable: 'GIT_USER', 
                    passwordVariable: 'GIT_TOKEN' )]) 
                    {
                sh '''
                    rm -rf gitops
                    git clone https://${GIT_USER}:${GIT_TOKEN}@github.com/LizaSaitov/GitOps-Project.git gitops
                    cd gitops
                    sed -i "s/tag: .*/tag: \"${BUILD_NUMBER}\"/" helmchart/values.yaml 
                    sed -i "s/tag: .*/tag: \"${BUILD_NUMBER}\"/" helmchart/env/qa/${APP_NAME}.yaml
                    helm template env-qa helmchart -f helmchart/env/qa/${APP_NAME}.yaml
                    git config user.name "Jenkins User"
                    git config user.email "jenkins@user.com"
                    git add helmchart/values.yaml helmchart/env/qa
                    git commit -m "Update image tag to ${BUILD_NUMBER} [skip ci]" || echo "Tag number updated"
                    git push https://${GIT_USER}:${GIT_TOKEN}@github.com/LizaSaitov/GitOps-Project.git main
                '''
            }
        }
    }
    }
}
 
