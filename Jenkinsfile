pipeline{
    agent any
    
    stages{
        stage('Code'){
            steps{
                echo "Cloning the code"
                git url:"https://github.com/useraikl/django-notes-app.git" , branch: "main"
            }
        }
        stage('Build'){
            steps{
            echo "Building the code"
            sh 'docker build -t notes-app .'
            }
        }
        stage('Push to Docker hub'){
            steps{
            echo "Pushing the code"
            withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerhubPass",usernameVariable:"dockerhubUname")]){
            sh "docker tag notes-app ${env.dockerhubUname}/notes-app:latest2"    
            sh "docker login -u ${env.dockerhubUname} -p ${env.dockerhubPass}"
            sh "docker push ${env.dockerhubUname}/notes-app:latest2"
               }
            }
        }
        stage('Deploy'){
            steps{
            echo "Deploying the code"
            sh "docker-compose down && docker-compose up -d"
            }
        }
    }
    
}
