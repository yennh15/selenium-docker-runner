pipeline{

    agent any

    stages{
        stage('Start Grid'){
            steps{
                sh "docker-compose -f grid.yaml up -d"
            }
        }

        stage('Run Test'){
            steps{
                sh "docker-compose -f test-suite.yaml up --pull=always"
                script {
                    if(fileExists('output/flight-resvervation/testng-failed.xml') || fileExists('output/vendor-portal/testng-failed.xml')){
                        error('failed tests found')
                    }
                }
            }
        }
    }
    post{
        always{
            sh "docker-compose -f grid.yaml down"
            sh "docker-compose -f test-suite.yaml down"
            archiveArtifacts artifacts: 'output/flight-resvervation/emailable-report.html', followSymlinks: false
        }
    }


}