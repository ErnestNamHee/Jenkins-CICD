pipeline  {
    agent any

    environment {
        FE_SWR_CREDENTIALS_LOGIN    = credentials('fe-swr-credential-login')
        FE_SWR_CREDENTIALS_PASSWORD = credentials('fe-swr-credential-password')
        FE_SWR_URL = "registry.eu-west-0.prod-cloud-ocb.orange-business.com"
    }

    stages {
        stage ('Build') {
            steps {
                echo "Building the Docker Image"
                //def customImage = docker.build("my-nginx:${env.BUILD_ID}")        
                sh "docker build -t ${FE_SWR_URL}/ernest/my-nginx:${env.BUILD_ID} ."
            }
        }
        stage ('Register') {
            steps {
                echo "Register the Docker Image to SWR"              
                sh "docker login -u $FE_SWR_CREDENTIALS_LOGIN -p $FE_SWR_CREDENTIALS_PASSWORD registry.eu-west-0.prod-cloud-ocb.orange-business.com"
                sh "docker push registry.eu-west-0.prod-cloud-ocb.orange-business.com/ernest/my-nginx:${env.BUILD_ID}"
            }
        }

        stage ('Deploy') {
            steps {
                echo "Deploy the Docker Images to CCR"              
            }
        }
    }

}

