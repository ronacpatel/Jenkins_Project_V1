pipeline {
    agent {
        // Use any node with the label 'docker'
        label 'docker'
            }
    stages {
        stage('Build') {
            steps {
                // Build the image from the Dockerfile in the current directory
                script {
                    def dockerImage = docker.build("my-image:${env.BUILD_ID}")
                    }
                    }
        }
        stage('Push') {
                steps {
                // Push the image to Docker Hub
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                        dockerImage.push()
                    }
                }
            }
        }
        stage('Test') {
            steps {
                sh 'node --version'
        }
    }
    
       stage('Build image') {
            steps {
                echo 'Starting to build docker image'

                script {
                    def customImage = docker.build("my-image:${env.BUILD_ID}")
                    customImage.push()
                }
            }
        }
      }
    }
       