pipeline {
  agent any  // Use any available agent

  environment {
    DOCKER_IMAGE = 'hassan085/dockerized-node-app'
  }

  stages {
    stage('Clone Repository') {
      steps {
        // Pull code from GitHub
        git branch: 'main', url: 'https://github.com/HassanGhafoor/jenkins-docker-revision'
      }
    }

    stage('Build Docker Image') {
      steps {
        // Build the Docker image using Windows Batch
        bat 'docker build -t %DOCKER_IMAGE% .'
      }
    }

    stage('Push Docker Image') {
      steps {
        script {
          withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'DOCKER_CREDENTIALS_USR', passwordVariable: 'DOCKER_CREDENTIALS_PSW')]) {
            // Log in to Docker Hub using the credentials injected from Jenkins
            bat '''
              echo %DOCKER_CREDENTIALS_PSW% | docker login -u %DOCKER_CREDENTIALS_USR% --password-stdin
              docker push %DOCKER_IMAGE%
            '''
          }
        }
      }
    }
  }
}
