pipeline {
    agent any

    stages {
        stage('Checkout and Dependencies') {
            steps {
                script {
                    git branch: 'main', url: 'YOUR_GIT_URL' // Replace with your Git repository URL
                }
                sh 'python3 -m venv venv' // Use Python 3 for consistency (adjust if needed)
                sh 'source venv/bin/activate && pip install -r requirements.txt' // Activate virtual environment and install dependencies
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
                expression { // Define conditions for running this stage (e.g., branch name, environment variable)
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
            cleanWs() // Clean workspace after build
        }
    }
}
