pipeline {
    agent any

    stages {
        
        stage ('Build Docker Image') {
            steps {
                script {
                    dockerapp = docker.build("leandromliveira/kube-news:${env.BUILD_ID}", '-f ./src/Dockerfile ./src')
                }
            }
        }

        stage ('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        dockerapp.push('latest')
                    }
                }
            }
        }

        stage ('Deploy kubernetes') {
            steps {
                withKubeconfig ([credentialsId: 'kubeconfig']) {
                    sh 'kubectl apply -f ./k8s/deployment.yaml'
                }
            }
        }
    }
}
