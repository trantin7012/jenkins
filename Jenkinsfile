pipeline {
    agent any
    stages {
        stage("Build image"){
            steps{
                sh 'docker build . -t trantin7012/testjenkin'
            }
        }
        stage("login"){
            steps{
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credential', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) 
                {
                sh 'echo $DOCKER_PASSWORD | docker login --username $DOCKER_USERNAME --password-stdin'
                }
            }
        }
        stage("push image"){
           steps{
                sh 'docker push trantin7012/testjenkin'
                sh 'docker image rm trantin7012/testjenkin'
           }
        }
        stage("deploy"){
            options {
                timeout(time: 10, unit: 'MINUTES')
            }
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credential', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) 
            }
        }
        stage("Build"){
            steps {
                sh "echo hello"
            }
        }
    }
}
