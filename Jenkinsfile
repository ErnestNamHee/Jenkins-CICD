node {
    checkout scm
    environment {
        FE_SWR_CREDENTIALS_LOGIN    = credentials('FE_SWR_CREDENTIALS_LOGIN')
        FE_SWR_CREDENTIALS_PASSWORD = credentials('FE_SWR_CREDENTIALS_PASSWORD')
    }

    parameters {
        string (name: 'FE_SWR_ENDPOINTS', defaultValue:'registry.eu-west-0.prod-cloud-ocb.orange-business.com', description: 'SWR URL Endpoint')
    }
    stage ('Build Docker Image') {
        def customImage = docker.build("my-nginx:${env.BUILD_ID}")        
        sh "docker build -t ${params.FE_SWR_ENDPOINTS}/ernest/my-nginx:${env.BUILD_ID} ."

    }
    stage ('Archive Docker Image to SWR') {
        sh "docker login -u $FE_SWR_CREDENTIALS_LOGIN -p $FE_SWR_CREDENTIALS_PASSWORD registry.eu-west-0.prod-cloud-ocb.orange-business.com"
        sh "docker push registry.eu-west-0.prod-cloud-ocb.orange-business.com/ernest/my-nginx:${env.BUILD_ID}"
    }

    stage ('Deploy Docker Image to CCE') {
        sh "docker push registry.eu-west-0.prod-cloud-ocb.orange-business.com/ernest/my-nginx:${env.BUILD_ID}"
    }
    
}

