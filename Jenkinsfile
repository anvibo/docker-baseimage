pipeline {
    agent any
    stages {

        stage('Clone repository') {
            steps {
                git credentialsId: 'github-anvibo', url: 'https://github.com/anvibo/docker-baseimage.git'
            }
        }

        stage('Build image 18.04 from master') {
            when { branch 'master' }
            steps {
                script {
                    def tag = "18.04"
                    app = docker.build("anvibo/baseimage", "-f ${tag}/Dockerfile .")

                    withDockerRegistry([url: "", credentialsId: "dockerhub-anvibo"]) {
                    app.push("${tag}")
                    app.push("${tag}-${env.BUILD_NUMBER}")
                    app.push("latest")
                    }
                }
            }
        }

        stage('Build image 18.04 from branch') {
            when { not { branch 'master' } }
            steps {
                script {
                  def tag = "18.04"
                  app = docker.build("anvibo/baseimage", "-f ${tag}/Dockerfile .")

                  withDockerRegistry([url: "", credentialsId: "dockerhub-anvibo"]) {
                  app.push("${tag}-${env.BRANCH_NAME}")
                  app.push("${tag}-${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                  }
                }
            }
        }

        stage('Build image 14.04 from master') {
            when { branch 'master' }
            steps {
                script {
                    def tag = "14.04"
                    app = docker.build("anvibo/baseimage", "-f ${tag}/Dockerfile .")

                    withDockerRegistry([url: "", credentialsId: "dockerhub-anvibo"]) {
                    app.push("${tag}")
                    app.push("${tag}-${env.BUILD_NUMBER}")
                    app.push("latest")
                    }
                }
            }
        }

        stage('Build image 14.04 from branch') {
            when { not { branch 'master' } }
            steps {
                script {
                  def tag = "14.04"
                  app = docker.build("anvibo/baseimage", "-f ${tag}/Dockerfile .")

                  withDockerRegistry([url: "", credentialsId: "dockerhub-anvibo"]) {
                  app.push("${tag}-${env.BRANCH_NAME}")
                  app.push("${tag}-${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                  }
                }
            }
        }
      }
}
