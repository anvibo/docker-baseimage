node {
    def app
parameters {
gitParameter name: 'TAG', type: 'PT_TAG', defaultValue: ''
}

    stage('Clone repository') {
        checkout scm
    }

    stage('Build image 18.04') {

        app = docker.build("anvibo/baseimage", "-f 18.04/Dockerfile .")

	withDockerRegistry([url: "", credentialsId: "dockerhub-anvibo"]) {
                app.push("18.04${params.TAG}")
                app.push("latest")

	}
}

	stage('Build image 14.04') {

        app = docker.build("anvibo/baseimage", "-f 14.04/Dockerfile .")
        
	withDockerRegistry([url: "", credentialsId: "dockerhub-anvibo"]) {
	
		app.push("14.04${params.TAG}")
	}
    }
}

