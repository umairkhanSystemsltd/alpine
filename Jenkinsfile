pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('darinpope-dockerhub')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t umairkhansystemsltd/alpine:latest .'
      }
    }
    stage('Scan') {
      steps {
        sh 'docker scan umairkhansystemsltd/alpine:latest'
      }
    }
    stage('Publish') {
      steps {
        sh '''
          docker login -u $DOCKERHUB_CREDENTIALS_USR -p $DOCKERHUB_CREDENTIALS_PSW
          docker push umairkhansystemsltd/alpine:latest
          docker logout
        '''
      }
    }
  }
}
