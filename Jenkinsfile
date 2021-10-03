pipeline {
    agent any
    environment {
      dockerImage = ''
      registry = custom
    }
    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Sarpit/jenkins-docker.git']]])
            }
        }
        stage('Docker Build Image') {
                steps {
                    script {
                        dockerImage = docker.build registry
                    }
                }
            }
    }
}
