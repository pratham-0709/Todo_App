pipeline{
    agent {
        node {
            label 'Linux'
        }
    }
    environment {
        registry = 'monsternex007/todos-app'
        registryCredential = 'Dockerhub'
        dockerImage = ''
    }
    stages{
        stage("Gather"){
            steps{
                git 'https://github.com/pratham-0709/Todo_App.git'
                sh 'sudo ls -la'
                sh 'sudo sleep 5'
            }
        }
        stage("Build"){
            steps{
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage("Deploy"){
            steps{
              sh 'sudo docker images'
              sh 'sudo docker run --name TodoApp -p 8000:8000 -d "$registry:$BUILD_NUMBER"'
              sh 'sudo docker ps'  
            }
        }
        stage("PUSH TO REGISTRY"){
            steps{
                script{
                    withDockerRegistry(credentialsId: 'DockerHubDetails') 
                    {
                        dockerImage.push()
                    }
                }
            }
        }
    }
    post{
        success{
            echo "Deployment Success"
        }
        failure{
            echo "Deployment Failed"
        }
    }
}
