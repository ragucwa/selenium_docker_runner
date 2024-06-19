pipeline{
    agent any
    stages{
        stage('Start grid'){
            steps{
                bat "docker-compose -f grid.yaml up -d"
            }
        }
        stage('Run tests'){
            steps{
                bat "docker-compose -f test-suites.yaml up --exit-code-from test-suites"
            }
        }
    }
    post{
        always{
            bat "docker-compose -f grid.yaml down"
            bat "docker-compose -f test-suites.yaml down"
        }
    }
}
