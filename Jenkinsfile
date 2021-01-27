node {
    checkout scm

    def customImage = docker.build("my-nginx:${env.BUILD_ID}")

    customImage.inside {
        //sh 'bash'
    }
}

