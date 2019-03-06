pipeline {
  agent any
  stages {
    stage('Checkout Sources') {
      steps {
        git(url: 'https://github.com/bepoland-academy/configuration-service.git', branch: 'development')
      }
    }
    stage('Compile') {
      steps {
        sh 'mvn clean install'
      }
    }
    stage('Build Docker Image') {
      steps {
        sh 'docker build -t pl.betse.beontime/configuration-service:latest .'
      }
    }
    stage('Tag Docker Image') {
      steps {
        sh '''docker tag pl.betse.beontime/configuration-service:latest build-server:5000/pl.betse.beontime/configuration-service
'''
      }
    }
    stage('Push Docker Image') {
      steps {
        sh 'docker push build-server:5000/pl.betse.beontime/configuration-service'
      }
    }
    stage('Checkout Deployment Config') {
      steps {
        git(url: 'https://github.com/bepoland-academy/deployment-configuration.git', branch: 'development')
      }
    }
    stage('Docker compose Pull') {
      steps {
        sh 'docker-compose -H main-server:2376 -f production/docker-compose.yml pull'
      }
    }
  }
}
