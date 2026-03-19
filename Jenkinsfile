pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
                // This pulls the latest index.html and Dockerfile from your Repo
                git branch: 'main', url: 'https://github.com/Jsriaws/ambank-web-app.git'
            }
        }
        stage('Clean Old Container') {
            steps {
                sh 'docker rm -f my-web-site || true'
            }
        }
        stage('Build Docker Image') {
            steps {
                // Now we just build using the files already in the workspace
                sh 'docker build -t my-custom-web:latest .'
            }
        }
        stage('Deploy to Production') {
            steps {
                sh 'docker run -d --name my-web-site -p 80:80 my-custom-web:latest'
            }
        }
    }
}
