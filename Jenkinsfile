pipeline {
  agent any
  stages {
    stage('Checkout and Dependencies') {
      steps {
        script {
          git url: 'https://github.com/egbeyon/curr_rates', branch: 'main'
        }

        sh 'python3 -m venv venv'
        sh 'source venv/bin/activate && pip install -r requirements.txt'
      }
    }

    stage('Run Tests') {
      steps {
        script {
          sh 'source venv/bin/activate && pytest -v' // Run tests with virtual environment activated
        }

      }
    }

    stage('Build and Push Docker Image (Optional)') {
      when {
        expression {
          return branch == 'master' || env.BUILD_DOCKER == 'true' // Example conditions
        }

      }
      steps {
        script {
          docker login -u $ACR_USERNAME -p $ACR_PASSWORD flaskdockerdemojeff.azurecr.io // Use environment variables for credentials
          sh 'docker build -t flaskdockerdemojeff/flask-rates-api .'
          sh 'docker push flaskdockerdemojeff.azurecr.io/flask-rates-api:latest'
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