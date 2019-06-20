pipeline {
   environment {
    registry = "anvibo/baseimage"
    registryCredential = 'dockerhub'
    dockerImage = ''
    tag = ''
  }

  agent {
    kubernetes {
      label 'jenkins-docker'
      yaml """
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: docker
    image: docker:1.11
    command: ['cat']
    tty: true
    volumeMounts:
    - name: dockersock
      mountPath: /var/run/docker.sock
  volumes:
  - name: dockersock
    hostPath:
      path: /var/run/docker.sock
"""
    }
  }
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/anvibo/docker-baseimage.git'
      }
    }
    stage('Build image 18.04' ) {
      steps{
        container('docker') {
                withDockerRegistry(registry: [credentialsId: 'dockerhub']) {
                  script {
                    dockerImage = docker.build(registry, "-f Dockerfile.18.04 .")
                  }
                }
            }
      }
    }
    stage('Push image 18.04') {
      steps{
        container('docker') {
                withDockerRegistry(registry: [credentialsId: 'dockerhub']) {
                  script {
                    dockerImage.push("18.04")
                    sh "docker rmi $registry:18.04"
                  }
                }
            }
      }
    }
    stage('Push release image 18.04') {
      when { tag "v*" }
      steps{
        container('docker') {
                withDockerRegistry(registry: [credentialsId: 'dockerhub']) {
                  script {
                    dockerImage.push("18.04")
                    dockerImage.push("18.04-$TAG_NAME")
                    sh "docker rmi $registry:18.04-$TAG_NAME"
                    sh "docker rmi $registry:18.04"
                  }
                }
            }
      }
    }
  }
}
