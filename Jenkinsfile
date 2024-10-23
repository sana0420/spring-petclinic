#!groovy

pipeline {
  agent none
  stages {
    stage('Maven Install') {
      agent {
            docker {
                  image 'maven:3.5.0'
                  args '-v $HOME/.m2:/root/.m2' // Optional: cache Maven dependencies
            }
      }
      steps {
        sh 'mvn clean install'
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
