pipeline {
    agent {
        label 'Agent1'
    }
    stages{
         stage("Clone"){
            steps{
                git url : "https://github.com/Mahak0301/django-notes-app.git" , branch: "main"
            }
         }
         stage("Build"){
            steps{
                echo "Building an image"
                sh "sudo docker build -t my-notes-app ."
            }
        }
         stage("Push to DockerHub"){
            steps{
                echo "Push to DockerHub"
                withCredentials([usernamePassword(credentialsId:"DockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "sudo docker tag my-notes-app ${env.dockerHubUser}/my-notes-app:latest"
                sh "sudo docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "sudo docker push ${env.dockerHubUser}/my-notes-app:latest"
                }
            }
        }
        stage("Deploy"){
            steps{
                echo "Deploy"
                sh "sudo docker run -d -p 8001:8000 my-notes-app"
            }
        }
        
    }
}

