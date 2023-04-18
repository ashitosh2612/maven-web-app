pipeline{
    agent{
        label "dev"
    }
    stages{
        stage("code clone "){
            steps{
            git 'https://github.com/ashitosh2612/maven-web-app.git'
            }
            
        }
    
    stage("maven build"){
        steps{
            sh """
            mvn clean package
            """
        }
    }
   stage("code review"){
    steps{
        script{
        withSonarQubeEnv(credentialsId: 'sonar') {
      sh 'mvn clean package sonar:sonar'
                }
    }
   }
   }
   stage("Artifact upload"){
    steps{
        script{
      nexusArtifactUploader artifacts: 
      [
        [
            artifactId: '01-maven-web-app',
             classifier: '', 
             file: 'target/01-maven-web-app.war',
              type: 'war'
              ]
              ],
               credentialsId: 'nexus',
               groupId: 'in.ashokit',
               nexusUrl: 'http://34.118.132.107:8081/', 
               nexusVersion: 'nexus3', 
               protocol: 'http', 
               repository: 'java_application', 
               version: '1.0-SNAPSHOT'
    }
   }
   }


   
    }
   }
