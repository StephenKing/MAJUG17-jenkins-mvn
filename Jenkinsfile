pipeline {
  agent any

  tools {
    maven 'maven-3'
  }

  stages {

    stage ('Clean') {
      steps {
        sh 'mvn clean'
      }
    }

    stage ('Build') {
      steps {
        sh 'mvn package'
      }

      post {
          success {
              junit 'target/surefire-reports/**/*.xml'
          }
      }
    }

    stage ('Archive') {
      steps {
        archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
      }
    }
  }
}