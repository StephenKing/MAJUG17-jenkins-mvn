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
    }

    stage ('Archive') {
      steps {
        archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
      }
    }
  }
}