pipeline {
    agent any
    stages {
        stage("code"){
            steps{
                
                git url: "https://github.com/Nishantyadav289/node-todo-cicd",branch: "master"
            }
           
        }
        stage("Buld and test"){
             steps{
                 sh "docker build . -t node-app-demo"
                 
             }
            
        }
        stage("push to repo"){
             steps{ 
                 withCredentials([usernamePassword(credentialsId:"mydockerhub",passwordVariable:"pass",usernameVariable:"user")]){
                     sh "docker login -u ${env.user} -p ${env.pass}"
                     sh "docker tag  node-app-demo ${env.user}/node-app-demo:latest"
                     sh "docker push ${env.user}/node-app-demo:latest"
                 }
                 
         
             }
            
        }
        stage("deploy"){
             steps{
                 
                 sh "docker-compose down && docker-compose up -d"
             }
            
        }
        
        
    }
    
    
    
    
    
    
    
}
