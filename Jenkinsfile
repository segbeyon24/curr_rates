pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        git(url: 'https://github.com/egbeyon/curr_rates', branch: 'main')
      }
    }

  }
}