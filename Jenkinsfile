pipeline {
    agent any
    stages {
                stage('Build') {
                    agent {
                        docker { image 'maven:3.6.3-openjdk-11-slim' }
                    }
                        steps {
                            sh 'mvn -B -DskipTests clean package'
                            archiveArtifacts artifacts: 'target/examen-*-SNAPSHOT.jar', fingerprint: true
                        }
                }

        }
}
