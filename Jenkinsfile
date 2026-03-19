pipeline {
    agent any
    stages {
        stage('Clean Up') {
            steps {
                // Remove old container if it exists so we don't get 'Port already in use' errors
                sh 'docker rm -f my-web-site || true'
            }
        }
        stage('Build & Run') {
            steps {
                // 1. Create a simple HTML file
                sh 'echo "<h1>Welcome to AmBank DevOps Server - Managed by Terraform</h1>" > index.html'
                
                // 2. Create a Dockerfile on the fly
                sh 'echo "FROM nginx:alpine" > Dockerfile'
                sh 'echo "COPY index.html /usr/share/nginx/html/index.html" >> Dockerfile'
                
                // 3. Build the Image
                sh 'docker build -t my-custom-web:latest .'
                
                // 4. Run the Container on Port 80
                sh 'docker run -d --name my-web-site -p 80:80 my-custom-web:latest'
            }
        }
    }
}
