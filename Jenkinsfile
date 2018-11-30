node {
  def mvnHome
    stage('Prepare') {
      git 'https://github.com/Chitrajaiswal/game-of-life.git'
      mvnHome = tool 'localmaven'
    }

    stage ('Build'){
      echo 'Maven Build'
      sh 'mvn -f pom.xml clean package'
    }

    stage('Publish'){
      nexusArtifactUploader(
      artifacts: [
      [artifactId: 'gameoflife', classifier: '', file: 'gameoflife-web/target/gameoflife.war', type: 'war']
      ], 
      credentialsId: 'nexus', 
      groupId: 'com.wakaleo.gameoflife', 
      nexusUrl: '192.168.56.105:8081', 
      nexusVersion: 'nexus3', 
      protocol: 'http', 
      repository: 'maven-releases', 
      version: '1.3'  
      )
    }
}
