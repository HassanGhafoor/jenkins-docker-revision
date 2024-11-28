pipeline {
  agent any  // Use any available agent

  environment {
    DOCKER_IMAGE = 'hassan085/dockerized-node-app'
    DOCKER_CREDENTIALS = credentials('dockerhub-credentials')  // Replace with your Jenkins credential ID
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
        // Build the Docker image
        sh 'docker build -t $DOCKER_IMAGE .'
      }
    }

    stage('Push Docker Image') {
      steps {
        // Log in to Docker Hub and push the image
        sh '''
        echo $DOCKER_CREDENTIALS_PSW | docker login -u $DOCKER_CREDENTIALS_USR --password-stdin
        docker push $DOCKER_IMAGE
        '''
      }
    }
  }
}
