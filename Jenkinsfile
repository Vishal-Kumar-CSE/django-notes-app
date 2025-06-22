@Library('my-shared-lib')_

pipeline{
    agent any;
    stages{
        stage("Code"){steps{
	echo "Code stage"
	code_checkout("https://github.com/Vishal-Kumar-CSE/django-notes-app.git","main")
        }}
        stage("Build"){steps{
            docker_build("notes-app2","latest","kmvishal")
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
