pipeline {
    agent any

    tool {
        maven 'maven-3'
    }

    stages {
        stage("Build") {
            steps {
                sh 'mvn package -DskipTests'
            }
        }
    }
}