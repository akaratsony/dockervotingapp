pipeline {
    agent any
    stages {
        stage('Cloning the repository ') {
            steps {
                script {
                    sh 'sudo git clone https://github.com/dockersamples/example-voting-app.git'
                    sh 'ls  /var/lib/jenkins/workspace/buildsimplewebapp/example-voting-app/ '
                }
            }
        }
        stage('Building the voting app image ') {
            steps {
                script {
                    sh 'cat /var/lib/jenkins/workspace/buildsimplewebapp/example-voting-app/vote/Dockerfile'
                    sh 'docker build /var/lib/jenkins/workspace/buildsimplewebapp/example-voting-app/vote/ -t voting-app'
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
