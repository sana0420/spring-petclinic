#!groovy
pipeline {
    agent none
    stages {
        stage('Maven Install') {
            agent any
            steps {
                script {
                    docker.image('maven:3.5.0').inside('-v $HOME/.m2:/root/.m2') {
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
    post {
        always {
            echo 'Cleaning up workspace...'
            cleanWs() // Clean workspace after every run
        }
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check logs for details.'
        }
    }
}
