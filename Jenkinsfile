pipeline{
    agent any

    parameters{
        choice choices: ["chrome_grid", "firefox_grid"], description: 'Select the browse', name: 'BROWSER'
    }

    stages{
        stage('Start grid'){
            steps{
                bat "docker-compose -f grid.yaml up --scale ${params.BROWSER}=2 -d"
            }
        }
        stage('Run tests'){
            steps{
                bat "docker-compose -f test-suites.yaml up"
            }
        }
    }
    post{
        always{
            bat "docker-compose -f grid.yaml down"
            bat "docker-compose -f test-suites.yaml down"
            archiveArtifacts artifacts: 'results/**', allowEmptyArchive: true
            junit 'results/local_cart_items_suite/*.xml'
            junit 'results/local_login_suite/*.xml'
        }
    }
}
