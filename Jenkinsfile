pipeline {
    agent any

    stages {
        stage('Cloning') {
            steps {
                echo 'Cloning'
                git branch: 'main', url: 'https://github.com/Sarpit/jenkins-docker.git'
            }
        }
   }
}
