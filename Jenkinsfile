pipeline{
    agent any

    stages{
        stage("Sonar Quality check"){
            agent {
                docker {
                    image 'openjdk:11'
                }
                        
                  }
            steps{
                script{
                     withSonarQubeEnv(credentialsId: 'sonarsecrate') {
                      sh 'chmod +x gradlew'
                      sh './gradlew sonarqube'
                     }
                    }
                }
            }
        }
    }