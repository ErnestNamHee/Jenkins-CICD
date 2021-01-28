pipeline  {
    agent any

    environment {
        FE_SWR_CREDENTIALS_LOGIN    = credentials('fe-swr-credential-login')
        FE_SWR_CREDENTIALS_PASSWORD = credentials('fe-swr-credential-password')
        FE_SWR_URL = "registry.eu-west-0.prod-cloud-ocb.orange-business.com"
        FE_SWR_ORGANIZATION = "ernest"
        DOCKER_IMAGENAME = "my-nginx"
        
        
    }

    stages {
        stage ('Build') {
            steps {
                echo "Building the Docker Image"
                //def customImage = docker.build("my-nginx:${env.BUILD_ID}")        
                sh "docker build -t ${FE_SWR_URL}/${FE_SWR_ORGANIZATION}/${DOCKER_IMAGENAME}:${env.BUILD_ID} ."
            }
        }
        stage ('Register') {
            steps {
                echo "Register the Docker Image to SWR"              
                sh "docker login -u ${FE_SWR_CREDENTIALS_LOGIN} -p ${FE_SWR_CREDENTIALS_PASSWORD} ${FE_SWR_URL}"
                sh "docker push ${FE_SWR_URL}/${FE_SWR_ORGANIZATION}/${DOCKER_IMAGENAME}:${env.BUILD_ID}"
            }
        }

        stage ('Deploy') {
            steps {
                echo "Deploy the Docker Images to CCE"
                
                sh "sed -i 's/<IMAGES>/${FE_SWR_URL}/${FE_SWR_ORGANIZATION}/${DOCKER_IMAGENAME}:${env.BUILD_ID}/' *.yaml"
                sh "cat *.yaml"

                echo "begin to config kubenetes"
                
                kubernetesDeploy(
                    kubeconfigId: "fe-cce-kubeconfig",
                    configs: "nginx.yaml")
                
                echo "hooray, success"
                }
              
            }
    }
}