pipeline {
    agent any
    options {
        buildDiscarder(logRotator(numToKeepStr: '5', daysToKeepStr: '5'))
        timestamps()
    }
    environment {
        registry = 'vitexsoftware/multiflexi-demo'
        registryCredential = 'dockerhub-token'
    }

    stages {
      stage('Building image') {
        steps {
          script {
            dockerImage = docker.build registry + ":$BUILD_NUMBER"
          }
        }
      }
      stage('Deploy Image') {
        steps {
          script {
              docker.withRegistry('', registryCredential) {
              dockerImage.push()
              }
          }
        }
      }
    }
}
