pipeline {
    agent any

    stages {
        stage('Login to Docker') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'hubCred', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    script {
                        // Log in to Docker
                        sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
                        sh 'docker info | grep "prithvidev"'
                    }
                }
            }
        }

        stage('Build and Push Docker Image') {
            steps{
                withCredentials([usernamePassword(credentialsId: 'hubCred', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]){
                    script{
                        sh '''
                        echo "Tagging the image before pushing"
                        docker tag spering-template:latest $DOCKER_USERNAME/spering-template:v3.0
                        docker images
                        echo "Pushing the images to the Hub Repository"
                        docker push $DOCKER_USERNAME/spering-template:v3.0
                        sh ''' 
                    }
                }
            }
        }
    }
}
