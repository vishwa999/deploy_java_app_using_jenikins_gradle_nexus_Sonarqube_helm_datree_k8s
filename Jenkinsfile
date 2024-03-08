pipeline{
    agent any

    stages{
        stage("Sonar Quality check"){
            agent {
                // docker {
                //     image 'openjdk:11'
                // }
                             docker {
                                image 'maven'
                                args '-v $HOME/.m2:/root/.m2:z -u root'
                                reuseNode true
                              }
                  }
            steps{
                script{
                     withSonarQubeEnv(credentialsId: 'sonarJenkins') {
                      //sh 'chmod +x gradlew'
                      //sh './gradlew sonarqube'
                        sh "mvn sonar:sonar"
                    
                        timeout(time: 1, unit: 'HOURS') {
                           def qg = waitForQualityGate()
                          if (qg.status != 'OK') {
                                 error "Pipeline aborted due to quality gate failure: ${qg.status}"
                           }
                        }
		                    sh "mvn clean install"
                    }
                    }
                }
            }
        }
    }