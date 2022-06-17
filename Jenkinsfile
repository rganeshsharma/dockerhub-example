pipeline {
  agent { label 'jenkins' }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhubaccesstoken')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t rganeshsharma2489/docker-example:latest .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push rganeshsharma2489/docker-example:latest'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}
