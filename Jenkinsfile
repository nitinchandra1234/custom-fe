pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'your-docker-image-name'
        ECR_REGISTRY = 'your-ecr-registry-url'
        KUBECONFIG = '/path/to/your/kubeconfig'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Compile Dockerfile') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Push Docker Image to ECR') {
            steps {
                withAWS(region: 'your-region', credentials: 'your-aws-credentials') {
                    sh """
                        $(aws ecr get-login --no-include-email --region your-region)
                        docker tag $DOCKER_IMAGE:latest $ECR_REGISTRY:latest
                        docker push $ECR_REGISTRY:latest
                    """
                }
            }
        }

        stage('Deploy to EKS') {
            steps {
                sh """
                    kubectl config use-context your-context
                    kubectl set image deployment/your-deployment your-container=$ECR_REGISTRY:latest --kubeconfig=$KUBECONFIG
                """
            }
        }
    }
}
