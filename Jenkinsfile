pipeline {
  agent any

  environment {

    GITHUB_USER = credentials('GITHUB_USER')
    GITHUB_TOKEN = credentials('GITHUB_TOKEN')

    DOCKER_PASSWORD_TOKEN = credentials('DOCKER_PASSWORD_TOKEN')
    DOCKER_IMAGE = 'cesarapires/api-smart-ranking'
    DOCKER_VERSION = "1.0.${BUILD_NUMBER}"
  }

  stages {
    stage('Cloning repository...') {
      steps {
        sh "rm -rf api-smart-ranking"
          
        sh "git clone https://$GITHUB_USER:${GITHUB_TOKEN}@github.com/cesarapires/api-smart-ranking.git"
      }
    }

    stage('Building docker image...') {
      steps {
        script {
          dir('api-smart-ranking') {
            sh "docker build -t ${DOCKER_IMAGE}:${DOCKER_VERSION} ."
          }
        }
      }
    }

    stage('Testing...') {
      steps {
        echo "Testing image"
      }
    }

    stage('Pushing image...') {
      steps {
        sh "docker login -u cesarapires -p ${DOCKER_PASSWORD_TOKEN}"

        sh "docker push docker.io/${DOCKER_IMAGE}:${DOCKER_VERSION}"
      }
    }
  }
}
