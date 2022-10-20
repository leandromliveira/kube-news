pipeline {
    agent any

    stages {
        stage ('Build Docker Image') {
            steps {
                scripts {
                    dockerapp = docker.build("fabricioveronez/kube-news:${env.BUILD_ID}", '-f ./src/Dockerfile ./src')
                }
            }
        }
    }
}
