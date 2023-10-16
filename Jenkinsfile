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
        stage('Push') {
                steps {
                // Push the image to Docker Hub
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                        dockerImage.push()
                    }
                }
            }
        stage('Test') {
            steps {
                sh 'node --version'
        }
    }
    stage('Push image') {
              steps{
              docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') 
              {
            app.push("${env.BUILD_NUMBER}")
        }
    }
      stage('Trigger ManifestUpdate') {
                echo "triggering updatemanifestjob"
                build job: 'updatemanifest', parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
                 }
              }
            }
        }
    }
}
