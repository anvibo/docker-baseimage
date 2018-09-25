node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Build image 18.04') {

        app = docker.build("docker-image", "-f 18.04/Dockerfile .")
    }


    stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
       /* docker.withRegistry('https://docker.io', 'dockerhub-anvibo') { */
            /*	app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")*/
/*            	app.push("${env.BRANCH_NAME}")
            
       } */
    }
}
