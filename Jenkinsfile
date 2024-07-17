pipeline {
    agent any
    stages {
        stage("code"){
            steps{
                git(url: 'https://github.com/nigamchandan/node-todo-cicd.git', branch: 'master')
            }
        }
        stage("Deploye"){
            steps{
                sh "docker build . -t node-app-test-new"
            }
        }
        stage("Push to Repository"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker tag node-app-demo ${env.dockerHubUser}/node-app-test-new:latest"
                    sh "docker push ${env.dockerHubUser}/node-app-test-new:latest"
                }
            }
        }
        stage("Deploy"){
            steps{
                sh "docker compose down && docker compose up -d"
            }   
        }
    }
}
