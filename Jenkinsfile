pipeline {
    agent any
    stages {
        stage("Clone Code") {
            steps {
                echo "Cloning the code"
                git url: "https://github.com/Anilkumar4599/Project-1-Jenkins-Declarative-CI-CD-Pipeline-for-DevOps-Engineers.git", branch: "main"
            }
        }
        stage("Build") {
            steps {
                echo "Building the image"
                sh "docker build -t my-note-app ."
            }
        }
        stage("Push to Docker Hub") {
            steps {
                echo "Pushing the image to Docker Hub"
                withCredentials([usernamePassword(credentialsId: "dockerHub", passwordVariable: "dockerHubPass", usernameVariable: "dockerHubUser")]) {
                    sh "docker tag my-note-app ${env.dockerHubUser}/my-note-app:latest"
                    sh "docker login -u ${env.dockerHubUser} -p ${dockerHubPass}"
                    sh "docker push ${env.dockerHubUser}/my-note-app:latest"
                    sh "docker logout"
                }
            }
        }
        stage("Deploy") {
            steps {
                echo "Deploying the app"
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
