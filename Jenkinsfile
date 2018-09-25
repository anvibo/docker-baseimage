node {
    def app

    stage('Clone repository') {
        checkout scm

sh 'printenv'
    }

    stage('Build image 18.04') {

        app = docker.build("anvibo/baseimage", "-f 18.04/Dockerfile .")

	withDockerRegistry([url: "", credentialsId: "dockerhub-anvibo"]) {
                app.push("18.04-${env.BRANCH_NAME}")
                app.push("18.04")
                app.push("latest")

	}
}

	stage('Build image 14.04') {

        app = docker.build("anvibo/baseimage", "-f 14.04/Dockerfile .")
        
	withDockerRegistry([url: "", credentialsId: "dockerhub-anvibo"]) {
	
		app.push("14.04-${env.BRANCH_NAME}")
		app.push("14.04")
	}
    }
}

