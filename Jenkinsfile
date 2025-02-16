pipeline {
    agent any

    environment {
        AWS_ACCOUNT_ID = ''
        AWS_REGION = 'us-east-1'
        ECR_REPOSITORY = 'an-example-repository-for-testing'
        IMAGE_TAG = "latest"
        DOCKER_IMAGE_NAME = 'testing-application'
    }

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $DOCKER_IMAGE_NAME:$IMAGE_TAG .'
                }
            }
        }

        stage('Login To ECR') {
            steps {
                script {
                    sh '''
                        $(aws ecr get-login --no-include-email --region $AWS_REGION)
                    '''
                }
            }
        }

        stage('Tag Docker Image') {
            steps {
                script {
                    sh "docker tag $DOCKER_IMAGE_NAME:$IMAGE_TAG $AWS_ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com/$ECR_REPOSITORY:$IMAGE_TAG"
                }
            }
        }

        stage('Push to ECR') {
            steps {
                script {
                    sh "docker push $AWS_ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com/$ECR_REPOSITORY:$IMAGE_TAG"
                }
            }
        }
    }

    post {
        success {
            echo 'Image pushed to ECR successfully'
        }
        failure {
            echo 'There was an error during the pipeline execution.'
        }
    }
}