pipeline {
    agent any
    stages {
        stage('Build') { steps { sh 'echo "Building..." && sleep 2' } }
        stage('Test')  { steps { sh 'echo "Testing..." && sleep 2' } }
        stage('Docker Build') { 
            steps { 
                sh 'docker build -t myapp:${BUILD_NUMBER} - <<EOF\nFROM nginx\nCOPY . /usr/share/nginx/html\nEOF'
            } 
        }
        stage('Push to GitHub Packages') { 
            steps { 
                sh 'echo "Pushing image..."'
                sh 'docker tag myapp:${BUILD_NUMBER} ghcr.io/clouder-omkar97/myapp:${BUILD_NUMBER}'
                sh 'echo $GITHUB_TOKEN | docker login ghcr.io -u clouder-omkar97 --password-stdin'
                sh 'docker push ghcr.io/clouder-omkar97/myapp:${BUILD_NUMBER}'
            } 
        }
    }
}
