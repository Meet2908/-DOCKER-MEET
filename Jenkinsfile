pipeline {
    agent any
    
    // accessing the credentials from jenkins
    environment {
        DOCKERHUB = credentials('Docker_hub')
    }
    
    stages {
        // cloning the git repo
        stage('Checkout') {
            steps {
                git 'https://github.com/Meet2908/-DOCKER-MEET.git'
            }
        }
        // building the docker image, 
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t meet2908/c0883915_assignment_4:latest .'
            }
        }

        // login in to docker hub
        stage('Login to Docker Hub') {
            steps {
                sh 'echo $DOCKERHUB_PSW | docker login -u $DOCKERHUB_USR --password-stdin'
            }
        }
         // pushing the project image to docker hub
        stage('Push to Docker Hub') {
            steps {
                sh 'docker push meet2908/c0883915_assignment_4:latest'
            }
        }
    }
    
    post {
        success {
            echo 'Docker image successfully built and pushed to Docker Hub!'
        }
        failure {
            echo 'Failed to build or push Docker image to Docker Hub'
        }
        // logging out of the docker account once all things are done
        always {
            sh 'docker logout'
        }
    }
}