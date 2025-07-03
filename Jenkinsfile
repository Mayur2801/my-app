pipeline {
  agent any

  environment {
    IMAGE_NAME = "mayur2808/my-app"
    TAG = "latest"
  }

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/Mayur2801/my-app.git'
      }
    }

    stage('Build Docker Image') {
      steps {
        script {
          docker.build("${IMAGE_NAME}:${TAG}")
        }
      }
    }

    stage('Push Docker Image') {
      steps {
        script {
          docker.withRegistry('https://registry.hub.docker.com', 'dockerhub-creds-id') {
            docker.image("${IMAGE_NAME}:${TAG}").push()
          }
        }
      }
    }

    stage('Deploy Container') {
      steps {
        script {
          // Stop and remove existing container if it exists
          sh "docker rm -f my-app-container || true"

          // Run a new container
          sh "docker run -d --name my-app-container -p 3000:3000 ${IMAGE_NAME}:${TAG}"
        }
      }
    }
  }

  post {
    success {
      echo "CD Pipeline completed successfully!"
    }
    failure {
      echo " CI/CD Pipeline failed!"
    }
  }
}
