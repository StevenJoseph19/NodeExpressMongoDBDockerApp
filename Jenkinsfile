pipeline{

    environment{
            DOCKERHUB_CREDENTIALS=credentials('dockerhub')
    }

    agent any

    stages{

            stage('Cloning Git repository'){
                steps{
                    git([ url: 'https://github.com/StevenJoseph19/NodeExpressMongoDBDockerApp.git', branch: 'master'])
                }
            }

            stage('Building Image'){
                steps{
                    sh 'docker build -t stevesam/nodeapp:latest -f node.dockerfile .'
                }
            }

            stage('Login to DockerHub'){
                steps{
                    sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin '
                }

            }

            stage('Push Image to DockerHub'){
                steps{
                    sh 'docker push stevesam/nodeapp:latest'
                }
            }

            stage('Remove unused Docker Image'){
                steps{
                    sh 'docker rmi stevesam/nodeapp:latest'
                }
            }
    }

        post{
                always{
                    sh 'docker logout'
                    echo 'Current directory is..'
                    echo  pwd()
                }
            }
}