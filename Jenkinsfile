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
  }

  post {
    success {
      echo " CI/CD Pipeline completed successfully!"
    }
    failure {
      echo " CI/CD Pipeline failed!"
    }
  }
}
