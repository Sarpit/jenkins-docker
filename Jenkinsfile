pipeline {
    agent any
    environment {
      dockerImage = ''
      registry = 'arpitdoc/samplehttpd'
      registryCredential = 'dockerid'
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
                        dockerImage = docker.build registry + ":$BUILD_NUMBER"
                    }
                }
            }
        stage('Docker Push Image'){
            steps {
                script {
                        docker.withRegistry('',registryCredential) {
                        dockerImage.push()
                    }
                }
            }
        }
        stage('docker stop container') {
            steps {
                sh 'docker ps -f name=samplehttpd -q | xargs --no-run-if-empty docker container stop'
                sh 'docker container ls -a -fname=samplehttpd -q | xargs -r docker container rm'
         }
       }
      stage('Docker Run') {
            steps{
                script {
                dockerImage.run("-p 9090:80 --rm --name samplehttpd")
                }
           }  
      }
   }
}
