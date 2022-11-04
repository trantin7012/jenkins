pipeline {
    agent any
    stages {
        stage("Build image"){
            steps{
                sh 'docker build --pull --rm -f "Dockerfile" -t trantin7012/testjenkin'
            }
        }
        stage("push image"){
           steps{
                sh'docker push trantin7012/testjenkin'
           }
        }
        stage("Build"){
            steps {
                sh "echo hello"
            }
        }
    }
}
