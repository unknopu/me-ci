pipeline {
      agent any
      stages {
            stage('SonarQube analysis') {
                  environment {
                        def scannerHome = tool 'mySonarScanner';
                  }
                  steps {
                        withSonarQubeEnv('LocalSonarServer') {
                              sh '${scannerHome}/bin/sonar-scanner'
                        }
                  }
            }
      }
}

// pipeline {
//       agent any
//       stages {
//             stage('Init') {
//                   steps {
//                         echo 'Hi, this is Anshul from LevelUp360'
//                         echo 'We are Starting the Testing'
//                   }
//             }
//             stage('Build') {
//                   steps {
//                         echo 'Building Sample Maven Project'
//                         sh 'mvn -f pom.xml clean package'
//                         sh 'ls -lathr'
//                   }
//                   post {
//                         success {
//                               echo "Now Archiving the Artifacts...."
//                               archiveArtifacts artifacts: '**/**.jar'
//                         }
//                   }
//             }
//             stages('CODE ANALYSIS with SONARQUBE') {
//                   // environment {
//                   //       def scannerHome = tool 'mySonarScanner';
//                   // }
//                   // steps {
//                   //       withSonarQubeEnv('LocalSonarServer') {
//                   //             sh '''${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=simpleMaven \
//                   //                   -Dsonar.projectName=simpleMaven \
//                   //                   -Dsonar.projectVersion=1.0 \
//                   //                   -Dsonar.scanAllFiles=true'''
//                   //             timeout(time: 10, unit: 'MINUTES') {
//                   //                   waitForQualityGate abortPipeline: true
//                   //             }
//                   //       }
//                   // }
//             }
//       }
// }
//                                     // -Dsonar.host.url=http://3.111.25.69:9000 \
//                                     // -Dsonar.login=sqa_4175ed933fe7e354fbbba6e0eeca4df104a32b93 \

