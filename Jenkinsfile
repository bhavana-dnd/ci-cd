pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "<your-dockerhub-username>/ci-cd-app"
    }

    stages {

        stage('Clone') {
            steps {
                echo "Cloning repo..."
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Push to DockerHub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    sh '''
                    docker login -u $USER -p $PASS
                    docker push $DOCKER_IMAGE
                    '''
                }
            }
        }
    }
}
