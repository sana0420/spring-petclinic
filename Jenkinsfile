pipeline {
    agent none

    stages {
        stage('Maven Install') {
            agent any
            steps {
                script {
                    // Running Maven inside a Docker container
                    docker.image('maven:3.5.0').inside {
                        sh 'mvn clean install'
                    }
                }
            }
        }

        stage('Docker Build') {
            agent any
            steps {
                // Building the Docker image for the application
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
