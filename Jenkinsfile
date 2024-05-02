pipeline{
agent any
    stages{

    stage('Run Selenium Grid')
    {
        steps{
        script
        {
        bat "docker-compose -f grid.yml up -d"
        }
      }
    }

    stage('Run Test Cases')
    {
        steps{
        bat "docker-compose -f test-suites.yml up --pull=always"
        script{
            if(fileExists('results/testng-failed.xml'))
            {
                error('failed tests cases')
            }
                }
    }
    }
}
post{
   always{
   bat "docker-compose -f grid.yml down"
   bat "docker-compose -f test-suites.yml down"
   archiveArtifacts artifacts: 'results/emailable-report.html', fingerprint: true
    }
   }
}