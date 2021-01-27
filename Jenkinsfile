node {
    checkout scm

    docker.withRegistry('https://registry.eu-west-0.prod-cloud-ocb.orange-business.com', '6a6419a5-2a19-4d16-9139-22fec7fe05a3') {
        
        def customImage = docker.build("my-nginx:${env.BUILD_ID}")
        

        customImage.push("https://registry.eu-west-0.prod-cloud-ocb.orange-business.com/ernest/my-nginx:${env.BUILD_ID}")

    }
}

