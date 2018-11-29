pipeline {
  agent any
    tools { 
        maven 'localmaven' 
    }

    stages{
      stage('SCM') {
         steps {
            git url: 'https://github.com/Chitrajaiswal/game-of-life.git'
         }
      }
      stage ('Build'){
        steps{
	  echo 'Maven Build'
          sh 'mvn -f pom.xml clean compile'
        }
      }
      stage ('SonarQube'){
        steps{
           sh 'mvn sonar:sonar -Dsonar.host.url=http://192.168.56.107:9000'
        }
      }
    }
}    

