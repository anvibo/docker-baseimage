node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Build image') {

        app = docker.build("anvibo/baseimage")
    }


    stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
        /*docker.withRegistry('https://index.docker.io', 'dockerhub-anvibo') {*/
            /*	app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")*/
            	app.push("${env.BRANCH_NAME}")
            
        /*}*/
    }
}
