pipeline {
    agent any
    post {
      failure {
        updateGitlabCommitStatus name: 'build', state: 'failed'
      }
      success {
        updateGitlabCommitStatus name: 'build', state: 'success'
      }
    }
     options {
      gitLabConnection('gitlab')
    }
    triggers {
        gitlab(triggerOnPush: true, triggerOnMergeRequest: true, branchFilterType: 'All')
    }
    stages {

        stage('Clone repository') {
            steps {
            checkout scm
            }
        }

        stage('Build image 18.04 from master') {
            when { branch 'master' }
            steps {
                script {
                    app = docker.build("anvibo/baseimage", "-f 18.04/Dockerfile .")

                    withDockerRegistry([url: "", credentialsId: "dockerhub-anvibo"]) {
                    app.push("18.04")
                    app.push("latest")
                    }
                }
            }
        }

        stage('Build image 18.04 from branch') {
            when { not { branch 'master' } }
            steps {
                script {
                app = docker.build("anvibo/baseimage", "-f 18.04/Dockerfile .")

                withDockerRegistry([url: "", credentialsId: "dockerhub-anvibo"]) {
                app.push("18.04-${env.BRANCH_NAME}")
                app.push("18.04")
                app.push("latest")

                }
                }
            }
        }

        stage('Build image 14.04 from master') {
            when { branch 'master' }
            steps {
                script {
                    app = docker.build("anvibo/baseimage", "-f 14.04/Dockerfile .")

                    withDockerRegistry([url: "", credentialsId: "dockerhub-anvibo"]) {
                    app.push("14.04")
                    app.push("latest")
                    }
                }
            }
        }

        stage('Build image 14.04 from branch') {
            when { not { branch 'master' } }
            steps {
                script {
                app = docker.build("anvibo/baseimage", "-f 14.04/Dockerfile .")

                withDockerRegistry([url: "", credentialsId: "dockerhub-anvibo"]) {
                app.push("14.04-${env.BRANCH_NAME}")
                app.push("14.04")
                app.push("latest")

                }
                }
            }
        }
    }
}
