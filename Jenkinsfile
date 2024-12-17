pipeline {
  agent any
  stages {
    stage('Build docker Image') {
      steps {
        sh '''script {
          docker.build("weather-app", "-f Dockerfile .")
        }'''
        }
      }

    }
  }