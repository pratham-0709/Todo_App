pipeline{
    agent any
    environment {
    registry = "monsternex007/docker-test"
    registryCredential = 'Dockerhub'
    dockerImage = ''
  }
    stages{
        stage("GATHER") {
            steps{
                git 'https://github.com/pratham-0709/Todo_App.git'
                sh 'ls -la'
                sh 'sleep 5'
            }
        }
        stage("BUILD") {
            steps{
                script {
                dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage("PUSH TO REGISTRY") {
            steps{
                script{
                    withDockerRegistry(credentialsId: 'DockerHubDetails') 
                    {
                        dockerImage.push()
                    }
                }
            }
        }
        stage("DEPLOY"){
            steps{
                sh "docker rmi $registry:$BUILD_NUMBER"
            }
        }
    }
}

