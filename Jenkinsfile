pipeline{
    agent any
    stages{
        stage('Start grid'){
            steps{
                bat "docker-compose -f grid.yaml up -d"
            }
        }
        stage('Run login tests'){
            steps{
                bat "docker-compose -f test-suites.yaml up --exit-code-from login_suite"
            }
        }
        stage('Run cart tests'){
            steps{
                bat "docker-compose -f test-suites.yaml up --exit-code-from cart_items_suite"
            }
        }
    }
    post{
        always{
            bat "docker-compose -f grid.yaml down"
            bat "docker-compose -f test-suites.yaml down"
            archiveArtifacts artifacts: 'output/login-suite/emailable-report.html', followSymlinks: false
            archiveArtifacts artifacts: 'output/cart-items-suite/emailable-report.html', followSymlinks: false
        }
    }
}
