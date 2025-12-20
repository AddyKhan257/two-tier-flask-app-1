pipeline{
    
    agent any;
    
    
    stages{
        stage("code"){
            steps{
               git url: "https://github.com/AddyKhan257/two-tier-flask-app-1", branch: "master"
                }
        }
        stage("build"){
            steps{
                sh "docker build -t my-flask-app ."
                 }
        }
        stage("test"){
            steps{
                echo "tester dega"
                }
        }
        stage("push to docker hub"){
            steps{
                withCredentials([usernamePassword(
                    credentialsId:"DockerHubCreds",
                    passwordVariable: "dockerHubPass",
                    usernameVariable: "dockerHubUser"
                )]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker image tag my-flask-app ${env.dockerHubUser}/my-flask-app"
                sh "docker push  ${env.dockerHubUser}/my-flask-app:latest"
                }
            }
        }
        stage("deploy"){
            steps{
                sh "docker compose up -d --build flask-app"
                }
        }
    }

}
