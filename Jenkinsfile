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
        withSonarQubeEnv(credentialsId: 'sonar') {
      sh 'mvn clean package sonar:sonar'
                }
    }
   }


   
    }
   }
