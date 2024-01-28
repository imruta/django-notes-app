pipeline{
    agent any
    stages{
        stage('code clone')
        {
            steps{
                echo "This is code clone stage"
                git url: "https://github.com/imruta/django-notes-app.git", branch: "main"
            }
        }
        stage('code build')
        {
            steps{
                echo "This is code build stage"
                sh 'docker build -t django-note-app:latest .'
            }
        }
        stage('image push')
        {
            steps{
                echo "This is image push to dockerhub stage"
               
               
   withCredentials([usernamePassword(credentialsId: "dockerhub", passwordVariable: "dockerhubPass", 
                                     usernameVariable: "dockerhubUser")]) {
    sh "docker tag django-note-app:latest ${env.dockerhubUser}/django-note-app:latest"
    sh "docker login -u ${env.dockerhubUser} -p ${env.dockerhubPass}"
}

   
            }
        }
        stage('code deploy')
        {
            steps{
                echo "This is code deploy stage"
                sh "docker-compose down && docker-compose up -d "
            }
        }
    }
    
    
    
