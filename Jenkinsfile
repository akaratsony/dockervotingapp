pipeline {
    agent any
    stages {
        stage('Cloning the repository ') {
            steps {
                script {
                    sh 'mkdir sample-application'
                    sh 'cd sample-application/'
                    sh 'sudo git clone https://github.com/dockersamples/example-voting-app.git'
                    sh 'cd example-voting-app/ '
                    sh 'ls'
                }
            }
        }
        stage('Building the voting app image ') {
            steps {
                script {
                    sh 'cd vote/ '
                    sh 'cat Dockerfile'
                    sh 'docker build . -t voting-app'
                    sh 'docker images'
                }
            }
        }
        stage('Run the voting app  ') {
            steps {
                script {
                    sh 'docker run -p 5000:80 voting-app'
                }
            }
        }

    }
}
