pipeline {
    agent any
    stages {
        stage("Build image"){
            steps{
                sh 'sudo docker build . -t trantin7012/testjenkin'
            }
        }
        stage("push image"){
           steps{
                sh'sudo docker push trantin7012/testjenkin'
           }
        }
        stage("Build"){
            steps {
                sh "echo hello"
            }
        }
    }
}
