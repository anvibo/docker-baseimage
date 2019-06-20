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
        tag = '18.04'
      }
    }
    stage("Building image $tag" ) {
      steps{
        container('docker') {
                withDockerRegistry(registry: [credentialsId: 'dockerhub']) {
                  script {
                    dockerImage = docker.build(registry + ":$tag" , "-f Dockerfile.$tag .")
                  }
                }
            }
      }
    }
    stage("Push image 18.04 $tag") {
      steps{
        container('docker') {
                withDockerRegistry(registry: [credentialsId: 'dockerhub']) {
                  script {
                    dockerImage.push()
                  }
                }
            }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        container('docker') {
          sh "docker rmi $registry:$BUILD_NUMBER"
        }
      }
    }
  }
}
