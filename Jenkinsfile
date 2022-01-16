pipeline {
  agent any
  tools {
    maven 'maven-3.8.4'
  }
  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/djadk84/spring-petclinic.git'
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
        input 'De you approve the deployemt?'
        sh 'scp target/*.jar jenks:/opt/pet/'
        sh 'ssh jenks -t "nohup java -jar /opt/pet/spring-petclinic-1.5.1.jar &"'
        }
      }
  }
}