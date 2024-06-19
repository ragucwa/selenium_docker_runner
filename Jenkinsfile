pipeline{
    agent any
    stages{
        stage('Start grid'){
            steps{
                bat "docker-compose -f grid.yml up -d"
            }
        }
        stage('Run tests'){
            steps{
                bat "docker-compose -f test-suites.yml up --exit-code-from test-suites"
            }
        }
    }
    post{
        always{
            bat "docker-compose -f grid.yml down"
            bat "docker-compose -f test-suites.yml down"
        }
    }
}
