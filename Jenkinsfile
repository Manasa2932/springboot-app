pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'rajcosivadevops/cicdncplimage'
        DOCKER_TAG = 'latest'
    }

    stages {
       
       
      stage('Login to Azure & Push Image') {
    steps {
        withCredentials([usernamePassword(credentialsId: 'azure-credentials', usernameVariable: 'AZURE_CLIENT_ID', passwordVariable: 'AZURE_CLIENT_SECRET')]) {
            sh '''
            az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET --tenant <TENANT_ID>
            az acr login --name myacr998
            docker push myacr998.azurecr.io/aks-javapp:latest
            '''
        }
    }
}
     
      

        stage('Deploy Container') {
            steps {
                script {
                    sh "docker run -d -p 8081:9090 ${DOCKER_IMAGE}:${DOCKER_TAG}"

                }
            }
        }
    }
}
