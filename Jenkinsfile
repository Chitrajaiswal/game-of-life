node {
  def mvnHome
    stage('Prepare') {
      git 'https://github.com/Chitrajaiswal/game-of-life.git'
      mvnHome = tool 'localmaven'
    }

    stage ('Build'){
      echo 'Maven Build'
      sh 'mvn -f pom.xml clean compile'
    }

    stage ('SonarQube'){
       sh 'mvn sonar:sonar -Dsonar.host.url=http://192.168.56.107:9000'
    }

    stage('Publish'){
      nexusArtifactUploader {
        nexusVersion('nexus3')
        protocol('http')
        nexusUrl('192.168.56.105:8081')
        groupId('com.wakaleo.gameoflife')
        version('1.2')
        repository('maven-snapshots')
        credentialsId('nexus')
        artifact {
          artifactId('gameoflife')
          type('war')
          classifier('debug')
          file('gameoflife-web/target/gameoflife.war')
        }
      }
    }
}
