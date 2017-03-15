pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
        }
    }

    stages {
        stage('Checkout') {
            steps {
                git "https://github.com/StephenKing/MAJUG17-jenkins-mvn"
                sh 'mvn clean'
            }
        }
        stage("Build") {
            steps {
                sh 'mvn package -DskipTests'
            }
        }
        stage("Tests") {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/**/*.xml'
                }
            }
        }
    }
    post {
        success {
            archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true

            emailext (
                    subject: "SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
                    body: """SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]': Check console output at ${env.BUILD_URL}""",
                    to: 'mail@example.org'
            )
        }

        failure {
            emailext (
                    subject: "FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
                    body: """FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]': Check console output at ${env.BUILD_URL}""",
                    to: 'mail@example.org'
            )
        }
    }
}