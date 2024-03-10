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
                sh "docker-compose -f test-suite.yaml up -d"
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