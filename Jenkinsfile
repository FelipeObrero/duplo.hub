pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub-credential')
  }
  stages {
    stage('Build') {
      steps {
        bat 'docker build -t flofree/duplo-hub:vbat .'
      }
    }
    stage('Login') {
      steps {
        bat 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        bat 'docker push flofree/duplo-hub:vbat'
      }
    }
  }
  post {
    always {
      bat 'docker logout'
    }
  }
}