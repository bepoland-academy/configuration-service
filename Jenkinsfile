pipeline {
  agent any
  stages {
    stage('Checkout Sources') {
      steps {
        git(url: 'https://github.com/bepoland-academy/configuration-service.git', branch: 'development')
      }
    }
  }
}