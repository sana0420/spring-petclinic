#!groovy

pipeline {
  agent none
  stages {
    stage('Maven Install') {
      agent any
      steps {
        script {
        // Run Maven inside a Docker container
            docker.image('maven:3.5.0').inside {
            sh 'mvn clean install'
              }
         }
        }

    }
    stage('Docker Build') {
      agent any
      steps {
        sh 'docker build -t shanem/spring-petclinic:latest .'
      }
    }
  }
}
