pipeline {
    agent any
    stages {
        stage('Build') {
            agent {
                docker {
                    image 'docker:dind'
                    // Run the container on the node specified at the
                    // top-level of the Pipeline, in the same workspace,
                    // rather than on a new node entirely:
                    reuseNode true
                }
            }
            steps {
                sh 'docker build -t akingo:worker:1.0.0 docker/worker.Dockerfile'
            }
        }
    }
}
