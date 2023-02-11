pipeline {
      agent any
      stages {
            stage('Init') {
                  steps {
                        echo 'Hi, this is Anshul from LevelUp360'
                        echo 'We are Starting the Testing'
                  }
            }
            stage('Build') {
                  steps {
                        echo 'Building Sample Maven Project'
                        sh 'mvn -f pom.xml clean package'
                  }
                  post {
                        success {
                              echo "Now Archiving the Artifacts...."
                              archiveArtifacts artifacts: '**/*.war'
                        }
                  }
            }
            // stage('SonarQube analysis') {
            //       environment {
            //             scannerHome = tool 'mySonarScanner'
            //       }
            //       // If you have configured more than one global server connection, you can specify its name
            //       steps {
            //             withSonarQubeEnv('LocalSonarServer') { 
            //                   sh "${scannerHome}/bin/sonar-scanner"
            //             }
            //       }
            // }
            stage('CODE ANALYSIS with SONARQUBE') {
                        environment {
                              scannerHome = tool 'mySonarScanner'
                        }
                        steps {
                              withSonarQubeEnv('LocalSonarServer') {
                              sh '''${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=simpleMavenJenkins \
                                    -Dsonar.projectName=simpleMavenJenkins \
                                    -Dsonar.projectVersion=1.0 \
                                    -Dsonar.sources=src/ \
                                    -Dsonar.java.binaries=**/**.java'''
                              }
                              timeout(time: 10, unit: 'MINUTES') {
                                    waitForQualityGate abortPipeline: true
                              }
                        }
            }
      }
}