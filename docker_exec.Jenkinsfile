#!groovy
pipeline {
    agent none
    stages {
        stage('Run Container test') {
            agent { label "docker" }
            steps {
                script {
                    docker.withRegistry('http://repo.nerdtakula.local:5000', '--repo--credentials--') {
                        docker.image('software/tests:latest').pull()
                        docker.image('repo.nerdtakula.local:5000/software/tests:latest').withRun { c ->
                            sh "docker exec ${c.id} /bin/bash -c 'env'"
                            sh "docker exec ${c.id} /bin/bash -c 'AM_SERVER_ADDR=\"http://10.10.0.11:8080\" cucumber features -p default'"
                        }
                    }
                }
            }
        }
    }
}