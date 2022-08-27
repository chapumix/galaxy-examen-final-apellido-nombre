pipeline {
    agent any
    stages {
                stage('Build') {
                    agent {
                        docker { image 'maven:3.6.3-openjdk-11-slim' }
                    }
                        steps {
                            sh 'mvn -B -DskipTests package'
                            archiveArtifacts artifacts: 'target/*-SNAPSHOT.jar', fingerprint: true
                        }
                }

                stage('SonarQube') {
                                                steps {
                                                    script{
                                                        def scannerHome = tool 'sonarscaner';
                                                                            withSonarQubeEnv('sonar-server') {
                                                                                sh "${scannerHome}/bin/sonar-scanner \
                                                                                    -Dsonar.projectKey=labmaven01 \
                                                                                    -Dsonar.projectName=labmaven01 \
                                                                                    -Dsonar.sources=src/main \
                                                                                    -Dsonar.sourceEncoding=UTF-8 \
                                                                                    -Dsonar.language=java \
                                                                                    -Dsonar.tests=src/test \
                                                                                    -Dsonar.junit.reportsPath=target/surefire-reports \
                                                                                    -Dsonar.surefire.reportsPath=target/surefire-reports \
                                                                                    -Dsonar.jacoco.reportPath=target/jacoco.exec \
                                                                                    -Dsonar.java.binaries=`.` \
                                                                                    -Dsonar.java.coveragePlugin=jacoco \
                                                                                    -Dsonar.coverage.jacoco.xmlReportPaths=target/jacoco.xml \
                                                                                    -Dsonar.exclusions=**/*IT.java,**/*TEST.java,**/*Test.java,**/src/it**,**/src/test**,**/gradle/wrapper** \
                                                                                    -Dsonar.java.libraries=`.`"
                                                                                }
                                                                            }
                                                    }
                                                }
}
}
