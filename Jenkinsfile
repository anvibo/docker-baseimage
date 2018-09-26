pipeline {
    agent any

stages {
    stage('Clone repository') {
        checkout scm
    }

    stage('Build image 18.04') {
        when { branch 'master' }
        steps {
            app = docker.build("anvibo/baseimage", "-f 18.04/Dockerfile .")

            withDockerRegistry([url: "", credentialsId: "dockerhub-anvibo"]) {
            app.push("18.04")
            app.push("latest")

	        }
        }
    }

    stage('Build release image 18.04') {
        when { buildingTag() }
        steps {
            app = docker.build("anvibo/baseimage", "-f 18.04/Dockerfile .")

            withDockerRegistry([url: "", credentialsId: "dockerhub-anvibo"]) {
            app.push("18.04-${env.BRANCH_NAME}")
            app.push("18.04")
            app.push("latest")

	        }
        }
    }
}
}
