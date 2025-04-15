pipeline {
  agent any
  stages {
    stage('Clone repository') {
      steps {
        checkout scm
      }
    }

    stage('Build image') {
      steps {
        script {
          app = docker.build("${IMAGE_NAME}")
        }

      }
    }

    stage('Push image') {
      steps {
        script {
          docker.withRegistry('https://registry.hub.docker.com', "${DOCKER_CREDENTIALS_ID}") {
            app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
            app.push("${env.BRANCH_NAME}-latest")
          }
        }

      }
    }

  }
  environment {
    IMAGE_NAME = 'EndritHasani01/kiii-jenkins'
    DOCKER_CREDENTIALS_ID = 'dockerhub'
  }
}