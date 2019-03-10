pipeline {
  agent { docker 'maven:3.5-alpine' }
  stages {
    stage('checkout') {
      steps {
        git 'https://github.com/Dina-Ula/spring-petclinic.git'
      }
    }
    stage('Build') {
      steps {
        sh 'mvn clean package'
        junit '**/target/surefire-reports/TEST-*.xml'
        archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
      }
    }
    stage('Deploy') {
      steps {
        input 'Do you want to approve the deployment?'
        sh 'scp target/*.jar jenkins@ubuntu1:/opt/pet/'
        sh 'ssh jenkins@ubuntu1 "nohup java -jar /opt/pet/spring-petclinic-2.1.0.BUILD-SNAPSHOT.jar &"'
      }
    }
  }
}
