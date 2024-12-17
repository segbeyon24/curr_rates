pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        sh '''script {
          git(url: \'https://github.com/egbeyon/curr_rates\', branch: \'main\')
        }

        script{
        sh \'python3 -m venv venv\'
        sh \'source venv/bin/activate && pip install -r requirements.txt\'
        }'''
        }
      }

    }
  }