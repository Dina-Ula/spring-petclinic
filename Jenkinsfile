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
        echo 'Deploying...'
      }
    }
  }
}
