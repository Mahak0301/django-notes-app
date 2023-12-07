pipeline {
    agent any
    stages{
         stage("CLone"){
            steps{
                git url : "https://github.com/Mahak0301/django-notes-app.git" , branch: "main"
            }
         }
         stage("Build"){
            steps{
                echo "Building an image"
                sh "docker build -t my-notes-app ."
            }
        }
         stage("Push to DockerHub"){
            steps{
                echo "Push to DockerHub"
                withCredentials([usernamePassword(credentialsId:"DockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag my-notes-app ${env.dockerHubUser}/my-notes-app:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/my-notes-app:latest"
                }
            }
        }
        stage("Deploy"){
            steps{
                echo "Deploy"
                sh "docker run -d -p 8002:8000 my-notes-app"
            }
        }
        
    }
}

