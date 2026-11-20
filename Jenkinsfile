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

        stage('Archive JAR') {
            steps {
                archiveArtifacts artifacts: 'complete/target/*.jar', fingerprint: true
            }
        }

        stage('Upload JAR to Nexus') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'nexus-hw8-credentials',
                        usernameVariable: 'NEXUS_USER',
                        passwordVariable: 'NEXUS_PASS'
                    )
                ]) {
                    bat '''
                    curl --fail --show-error -u "%NEXUS_USER%:%NEXUS_PASS%" ^
                    --upload-file complete\\target\\spring-boot-complete-0.0.1-SNAPSHOT.jar ^
                    http://localhost:8085/repository/hw8-springboot-releases/com/example/spring-boot-complete/1.0.0/spring-boot-complete-1.0.0.jar
                    '''
                }
            }
        }
    }
}
