node {
    checkout scm

    docker.withRegistry('https://registry.eu-west-0.prod-cloud-ocb.orange-business.com', 'eu-west-0@WOYP9KUMUJT6BVSGZFRA') {
        
        def customImage = docker.build("my-nginx:${env.BUILD_ID}")
        
        customImage.push()

    }
}

