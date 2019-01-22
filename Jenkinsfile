pipeline {
    agent any
    stages {

        stage('Clone repository') {
            steps {
                git credentialsId: 'github-anvibo', url: 'https://github.com/anvibo/docker-baseimage.git'
            }
        }

           
      }
}
