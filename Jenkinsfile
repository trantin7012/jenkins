pipeline {
    agent any
    stages {
        stage("Build image"){
            dockerImage = docker.build("trantin7012/testjenkin:latest")
        }
        stage("push image"){
            withDockerRegistry([credentialsId:"docker-hub-credential",url:""])
            {dockerImage.push()
            }
        }
        stage("Build"){
            steps {
                sh "echo hello"
            }
        }
    }
}
