pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'docker build -t myapp:latest .'
            }
        }
        stage('Test') {
            steps {
                sh 'docker run -d --name myapp-test -p 8081:8080 myapp:latest'
                sh 'sleep 2'
                sh 'curl -s http://localhost:8081 || true'
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker rm -f myapp-prod || true'
                sh 'docker run -d --name myapp-prod -p 8082:8080 myapp:latest'
            }
        }
        stage('Cleanup') {
            steps {
                sh 'docker rm -f myapp-test || true'
            }
        }
    }
}
