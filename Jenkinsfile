pipeline{
    agent any

    parameters{
        choice choices: ["chrome", "firefox"], description: 'Select the browse', name: 'BROWSER'
        string name: 'TEST_GROUP', defaultValue: 'login', description: 'Select the test group'
    }

    stages{
        stage('Start grid'){
            steps{
                bat "docker-compose -f grid.yaml up --scale ${params.BROWSER}=2 -d"
            }
        }
        stage('Run tests') {
            steps {
                script {
                    def exitCode = bat(script: "docker-compose -f test-suites.yaml up --abort-on-container-exit", returnStatus: true)
                    echo "Exit Code: ${exitCode}"
                }       
            }
        }
    }
    post{
        always{
            bat "docker-compose -f grid.yaml down"
            bat "docker-compose -f test-suites.yaml down"
            archiveArtifacts artifacts: 'results/**', allowEmptyArchive: true
            junit 'results/test_suite/*.xml'
        }
    }
}
