pipeline {
    agent {
        label "agent"
        // docker { 
        //     image 'docker'
        //     args '--entrypoint='
        // }
    }
    stages {
        stage('Build') {
            steps {
                sh 'echo "Start build job"'
                sh 'pwd'
                sh 'ls -la'
                script {
                    sh 'docker build -f front/frontend/Dockerfile -t registry:5000/front ./front/frontend'
                    sh 'docker push registry:5000/front'
                    sh 'hostname'
                    sh 'cat /etc/hosts'
                    sh 'ip a'
                    sh 'ping registry'
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
