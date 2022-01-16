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
        echo "Deploying"
        }
      }
  }
}