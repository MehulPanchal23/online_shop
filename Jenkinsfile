pipeline{
    agent any;
    stages{
        stage("Code Clone from GITHUB"){
            steps{
                git url: "https://github.com/MehulPanchal23/online_shop.git", branch: "Hackathon"
            }
        }
        stage("build image"){
            steps{
                sh "docker build -t online_shop ."
            }
        }
        stage("Push Image to Docker HUB"){
            steps{
                withCredentials([usernamePassword(
                    credentialsId: "dockerhubcred",
                    passwordVariable: "dockerhubpass",
                    usernameVariable: "dockerhubuser"
                    )]){
                sh "docker login -u ${env.dockerhubuser} -p ${env.dockerhubpass}"
                sh "docker image tag online_shop ${env.dockerhubuser}/online_shop"
                sh "docker push ${env.dockerhubuser}/online_shop:latest"
                }
            }
        }
        stage("deployment"){
           steps{ 
               sh "docker compose up -d"
           }
        }
        
    }
}
