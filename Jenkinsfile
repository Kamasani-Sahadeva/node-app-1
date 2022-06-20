pipeline {
    agent any
    environment {

        DOCKER_TAG = getDockerTag()

    }
    stages {
        stage('Build docker image'){
            steps {
                sh 'docker build . -t 8919687630/node-image:${DOCKER_TAG}'    

            }
            
        }

        stage('Push images into Docker Hub'){
            steps{
                withCredentials([string(credentialsId: 'Dockerhub_cred', variable: 'DockerHubPwd')]) {
                sh 'docker login -u 8919687630 -p ${DockerHubPwd}'
                sh 'docker push 8919687630/node-image:${DOCKER_TAG}'
            }
                

            }
        }

    }
} 

    

def getDockerTag(){
    def tag = sh script: 'git rev-parse HEAD', returnStdout: true  
    return tag
}
