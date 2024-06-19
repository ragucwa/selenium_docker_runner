pipeline{
    agent any
    stages{
        stage('Run tests'){
            steps{
                bat "docker-compose up"
            }
        }
        stage('Bring grid down'){
            steps{
                bat 'docker-compose down'
            }
        }
    }
}
