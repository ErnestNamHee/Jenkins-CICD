node  {
    checkout scm
    environment {
        FE_SWR_CREDENTIALS_LOGIN    = credentials('FE_SWR_CREDENTIALS_LOGIN')
        FE_SWR_CREDENTIALS_PASSWORD = credentials('FE_SWR_CREDENTIALS_PASSWORD')
        def FE_SWR_URL = "registry.eu-west-0.prod-cloud-ocb.orange-business.com"
    }


    stage ('Build Docker Image') {
        def customImage = docker.build("my-nginx:${env.BUILD_ID}")        
        sh "docker build -t $FE_SWR_URL/ernest/my-nginx:${env.BUILD_ID} ."

    }
    stage ('Archive Docker Image to SWR') {
        sh "docker login -u $FE_SWR_CREDENTIALS_LOGIN -p $FE_SWR_CREDENTIALS_PASSWORD registry.eu-west-0.prod-cloud-ocb.orange-business.com"
        sh "docker push registry.eu-west-0.prod-cloud-ocb.orange-business.com/ernest/my-nginx:${env.BUILD_ID}"
    }

    stage ('Deploy Docker Image to CCE') {
        sh "docker push registry.eu-west-0.prod-cloud-ocb.orange-business.com/ernest/my-nginx:${env.BUILD_ID}"
    }
    
}

