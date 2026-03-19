pipeline {
    agent any
    stages {
        stage('Clean Up') {
            steps {
                sh 'docker rm -f my-web-site || true'
            }
        }
        stage('Build & Run') {
            steps {
                // 1. Force create the file in the CURRENT workspace folder
                sh 'echo "<h1>Welcome to AmBank DevOps - Version 2.0</h1>" > index.html'
                
                // 2. Build a fresh image (no cache) to ensure index.html is copied
                sh 'docker build --no-cache -t my-custom-web:latest .'
                
                // 3. Run the container
                sh 'docker run -d --name my-web-site -p 80:80 my-custom-web:latest'
            }
        }
    }
}
