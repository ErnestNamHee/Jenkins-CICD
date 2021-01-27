node {
    checkout scm

    stage ('Build Docker Image') {
        def customImage = docker.build("my-nginx:${env.BUILD_ID}")        
        sh "docker build -t registry.eu-west-0.prod-cloud-ocb.orange-business.com/ernest/my-nginx:${env.BUILD_ID} ."

    }
    stage ('Deploy Docker Image to SWR') {
        sh "docker login -u eu-west-0@WOYP9KUMUJT6BVSGZFRA -p dced103a844272d419895c17bb7d1f7d3fa54451ca41af70112eb08c097d805e registry.eu-west-0.prod-cloud-ocb.orange-business.com"
        sh "docker push registry.eu-west-0.prod-cloud-ocb.orange-business.com/ernest/my-nginx:${env.BUILD_ID}"
    }

    
}

