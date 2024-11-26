pipeline {
  agent any

  environment {
    COMPOSE_FILE = 'docker-compose.yml'
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build') {
      steps {
        script {
          sh 'docker-compose build'
        }
      }
    }

    stage('Test') {
      steps {
        script {
          sh 'docker-compose up -d'
          sh 'docker-compose exec <service_name> <test_command>'
        }
      }
    }

    stage('Teardown') {
      steps {
        script {
          sh 'docker-compose down'
        }
      }
    }
  }

  post {
    always {
      cleanWs()
    }
  }
}