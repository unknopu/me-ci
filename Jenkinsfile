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
                        sh 'ls -lathr'
                  }
                  post {
                        success {
                              echo "Now Archiving the Artifacts...."
                              archiveArtifacts artifacts: '**/**.jar'
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
                              sh '''${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=simpleMaven \
                                    -Dsonar.projectName=simpleMaven \
                                    -Dsonar.host.url=http://3.111.25.69:9000 \
                                    -Dsonar.projectVersion=1.0 \
                                    -Dsonar.scanAllFiles=true'''
                              }
                              timeout(time: 10, unit: 'MINUTES') {
                                    waitForQualityGate abortPipeline: true
                              }
                        }
            }
      }
}