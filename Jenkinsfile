pipeline {
    agent any
stages {
stage('Cloning our Git') {
steps {
git 'https://github.com/Victor-Krivonosov/micro-svc.git'
}
    agent any
    stages {
        stage('Build') {
            steps {
                sh echo "Start build job"
                script {
                  sh docker build -f frontend/Dockerfile -t 192.168.2.2:5000/front ./frontend
                  sh docker push 192.168.2.2:5000/front
                }
            }
        }
        stage('Test') {
            steps {
                sh "echo 'stage test'"
            }
        }
        stage('Deploy') {
            steps {
                sh "echo 'stage deploy'"
            }
        }
    }
}
