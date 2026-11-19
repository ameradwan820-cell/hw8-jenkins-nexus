pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                dir('complete') {
                    bat 'mvnw.cmd clean package'
                }
            }
        }
    }
}
