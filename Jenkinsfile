pipeline{
    agent {label "dev-agent"}
    stages{
        stage("code"){
            steps {
                git url: "https://github.com/hemantrautmale7777/node-todo-cicd.git", branch: "master"
            }
        }
        stage("build & test"){
            steps {
                sh "docker build . -t hemantrautmale7777/note-todo-app-cicd:latest"
            }
        }
        stage("logging and push image"){
            steps {
                echo "logging in docker hub and pushing image"
                withCredentials([usernamePassword(credentialsId: "dockerhub",passwordVariable:"dockerHubPassword", usernameVariable: "dockerHubUser")]) {
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                    sh "docker image push hemantrautmale7777/note-todo-app-cicd:latest "
                }
            }
        }
         stage("Deploy"){
            steps {
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
