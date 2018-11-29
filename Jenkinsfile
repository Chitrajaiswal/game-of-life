pipeline {
  agent any
    tools { 
        maven 'localmaven' 
	jdk 'localJDK'
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
      stage('Test') {
         steps {
            sh 'mvn test'
         }
         post {
           always {
              junit 'gameoflife-web/target/surefire-reports/*.xml'
	      junit 'gameoflife-core/target/surefire-reports/*.xml'
           }
         }
      }

    }
}    

