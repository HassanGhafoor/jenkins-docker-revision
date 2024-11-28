pipeline {
  agent any  // Use any available agent

  environment {
    DOCKER_IMAGE = 'hassan085/dockerized-node-app'
    DOCKER_USERNAME = 'hassan085'  // Your Docker Hub username
    DOCKER_PASSWORD = 'qwerty321'  // Your Docker Hub password (hardcoded for testing)
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
        // Hardcode login credentials and push the image using Windows Batch
        bat '''
        echo %DOCKER_PASSWORD% | docker login -u %DOCKER_USERNAME% --password-stdin
        docker push %DOCKER_IMAGE%
        '''
      }
    }
  }
}
