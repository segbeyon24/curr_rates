pipeline {
  agent any

  environment {
        // Define the path to your virtual environment
        VENV_PATH = 'venv'  // This will be the name of the virtual environment folder
        APP_DIR = '/path/to/your/flask/app'  // Path to your Flask app directory
    }
    
  stages {
    stage('Checkout') {
      steps {
        script {
          git(url: 'https://github.com/egbeyon/curr_rates', branch: 'main')
        }

        script{
        sh 'python3 -m venv venv'
        sh 'source venv/bin/activate && pip install -r requirements.txt'
        }
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
