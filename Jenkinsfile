node {
    def app1, app2

    stage('Clone repository') {
        checkout scm
    }

    stage('Build image 18.04') {

        app1 = docker.build("anvibo/baseimage", "-f 18.04/Dockerfile .")
	}

	stage('Build image 14.04') {

        app2 = docker.build("anvibo/baseimage", "-f 14.04/Dockerfile .")
        }

	stage ('pushing images to dockerhub') {
	withDockerRegistry([url: "", credentialsId: "dockerhub-anvibo"]) {
		app1.push("18.04")
		app1.push("latest")
		app2.push("14.04")
	}
    }
}

}
