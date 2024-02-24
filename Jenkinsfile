pipeline {
    agent {
//        label "agent"
        docker { 
            image 'docker'
            args '--entrypoint='
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'echo "Start build job"'
                script {
                  sh 'docker build -f frontend/Dockerfile -t 192.168.201.12:5000/front ./frontend'
                  sh 'docker push 192.168.201.12:5000/front'
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
