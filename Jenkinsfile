pipeline {
    agent {
        docker {
            image 'golang:latest'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    environment {
        DOCKER_HUB = credentials('dockerhub')
    }
    stages {
        stage('Build') {
            steps {
                sh 'docker build -t $DOCKER_HUB_USR/workerTest docker/helloworkflow.Dockerfile'
                sh 'docker build -t $DOCKER_HUB_USR/helloworkflowTest docker/helloworkflow.Dockerfile'
            }
        }
        stage('Push worker and helloworkflow to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'DOCKER_HUB_PASSWORD', usernameVariable: 'DOCKER_HUB_USERNAME')]) {
                    sh 'echo "$DOCKER_HUB_PASSWORD" | docker login --username "$DOCKER_HUB_USERNAME" --password-stdin'
                    sh 'docker push $DOCKER_HUB_USR/helloworkflowTest $DOCKER_HUB_USR/workerTest'
                }
            }
        }
        stage('Deploy temporal apps'){
            agent {
                docker {
                    image 'lachlanevenson/k8s-kubectl:v1.17.4'
                    args '-v /var/run/docker.sock:/var/run/docker.sock'
                }
            }
            steps {
                sh 'kubectl apply -f manifest.yml'
            }
        }
    }
}
