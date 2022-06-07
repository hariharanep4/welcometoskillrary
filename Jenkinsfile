pipeline {
  agent any
  
  stages {
    stage('Build') {
      steps {
        sh 'mvn clean install -DskipTests'
      }
      
      post {
        success {
          echo 'Archiving...'
          archiveArtifacts artifacts: '**/target/*.war'
        }
      }
    }
    
    stage('Unit Test') {
      steps {
        sh 'mvn test'
      }
    }
    
    stage('Integration Test') {
      steps {
        sh 'mvn verify -DskipUnitTests'
      }
    }
    
    stage('Code Analysis with Checkstyle') {
      steps {
        sh 'mvn checkstyle:checkstyle'
      }
      
      post {
        success {
          echo 'Generated Analysis Result'
        }
      }
    }
}
