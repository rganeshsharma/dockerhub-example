pipeline {
  agent { label 'jenkins' }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhubaccesstoken')
    OCKERHUB_CREDENTIALS_USR = 'ganeshsharma2489'
    DOCKERHUB_CREDENTIALS_PSW = 'cd3a3376-d598-4556-8698-6dbdea10da87'
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t rganeshsharma2489/docker-example:latest .'
      }
    }
    stage('Login') {
      steps {
        sh 'docker login -u $DOCKERHUB_CREDENTIALS_USR --password $DOCKERHUB_CREDENTIALS_PSW'
        sh echo 'login succesful'
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
