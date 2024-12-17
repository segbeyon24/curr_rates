pipeline {
  agent any
  stages {
    stage('Build Docker Image') {
      steps {
        script {
          docker.build("app", "-f Dockerfile .")
        }

      }
    }

    stage('Run Docker Container') {
      steps {
        sh 'docker run -d -p 5000:5000 app'
      }
    }

  }
  post {
    always {
      sh 'echo "Running on port 5000" '
    }

  }
}