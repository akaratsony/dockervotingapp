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
        stage('Building the voting app images ') {
            steps {
                script {
                    sh 'cat /var/lib/jenkins/workspace/buildsimplewebapp/example-voting-app/vote/Dockerfile'
                    sh 'sudo docker build /var/lib/jenkins/workspace/buildsimplewebapp/example-voting-app/vote/ -t voting-app'
                    sh 'cat /var/lib/jenkins/workspace/buildsimplewebapp/example-voting-app/worker/Dockerfile'
                    sh 'sudo docker build /var/lib/jenkins/workspace/buildsimplewebapp/example-voting-app/worker/ -t worker-app'
                    sh 'cat /var/lib/jenkins/workspace/buildsimplewebapp/example-voting-app/result/Dockerfile'
                    sh 'sudo docker build /var/lib/jenkins/workspace/buildsimplewebapp/example-voting-app/result/ -t result-app'
                    sh 'sudo docker images'
                    //download redis
                }
            }
        }
        stage('Run the voting app  ') {
            steps {
                script {
                    sh 'sudo docker run  -d --name=redis redis'
                    sh 'sleep 5'
                    sh 'sudo docker run  -d -p 5000:80 --link redis:redis voting-app'
                    sh 'sleep 5'
                    sh 'sudo docker run  -d --name=db postgres:15-alpine '
                    sh 'sleep 10'
                    sh 'sudo docker run -d --link redis:redis --link db:db worker-app'
                    sh 'sleep 5'
                    sh 'sudo docker run  -d -p 5001:80 --link db:db result-app'
                }
            }
        }

    }
}
