node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Build image 18.04') {

        app = docker.build("anvibo/baseimage", "-f 18.04/Dockerfile .")

	docker.withRegistry('https://docker.io', 'dockerhub-anvibo') {
		app.push("18.04")
	}
    }


    }
}
