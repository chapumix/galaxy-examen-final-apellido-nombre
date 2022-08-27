pipeline {
    agent any
    stages {
                stage('Build') {
                    agent {
                        docker { image 'maven:3.6.3-openjdk-11-slim' }
                    }
                        steps {
                            sh 'mvn -B -DskipTests clean package'
                            archiveArtifacts artifacts: 'target/*-SNAPSHOT.jar', fingerprint: true
                        }
                }

                stage('SonarQube') {
                                steps {
                                    script{
                                        def scannerHome = tool 'sonarscaner'
                                        withSonarQubeEnv('sonar-server') {
                                            sh "${scannerHome}/bin/sonar-scanner \
                                            -Dsonar.projectKey=labmaven \
                                            -Dsonar.projectName=labmaven \
                                            -Dsonar.java.binaries=build/classes \
                                        }
                                    }
                                }
                            }


        }
}
