pipeline{
    agent any
    stages{
        stage('verify installation'){
            steps{
                sh '''
                    docker version
                    docker info
                    docker compose version
                    curl --version
                    jq --version
                '''
            }
        }

        stage('Starting Container'){
            steps {
                sh 'docker compose up -d --no-color --wait'
                sh 'docker compose'
            }
        }

        stage('Testing against the container'){
            steps{
                sh 'curl http://localhost:3000/param?query=demo | jq'
            }
        }
    } 

    post {
        always{
            sh 'docker compose down --remove-orphans -v'
            sh 'docker compose ps'
        }
    }  
}    
