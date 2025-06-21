pipeline{
    agent any;
    stages{
        stage("Code"){steps{
            git url:"https://github.com/Vishal-Kumar-CSE/django-notes-app.git",branch:"main"
        }}
        stage("Build"){steps{
           sh "docker build -t notes-app2:latest ."
        }}
        stage("Push to Dockerhub"){steps{
           withCredentials([usernamePassword(
               credentialsId:"DockerHubPat",
               usernameVariable:"DockerhubUser",
               passwordVariable:"DockerhubPass")]){
               sh "docker login -u ${env.DockerhubUser} -p ${env.DockerhubPass}"
               sh "docker image tag notes-app2:latest ${env.DockerhubUser}/notes-app2:latest"
               sh "docker push ${env.DockerhubUser}/notes-app2:latest"
           }
        }}
        stage("Deploy"){steps{
            sh "date"
            sh "docker compose down && docker compose up -d"
        }}

    }
}
