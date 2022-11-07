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
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credential', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')])
                {
                    ansiblePlaybook(
                        credentialsId: 'ssh-key',
                        playbook: 'playbook.yml',
                        inventory: 'hosts',
                        become: 'yes',
                        extraVars: [
                            DOCKER_USERNAME: "${DOCKER_USERNAME}",  
                            DOCKER_PASSWORD: "${DOCKER_PASSWORD}" 
                        ]
                    )
                }

            }
        }
        stage("Build"){
            steps {
                sh "echo hello"
            }
        }
    }
}
