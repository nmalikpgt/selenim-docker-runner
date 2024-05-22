pipeline{
agent any
    stages{

    stage('Run Selenium Grid')
    {
        steps{
        script
        {
        sh "docker-compose -f grid.yml up -d"
        }
      }
    }

    stage('Run Test Cases')
    {
        steps{
        sh "docker-compose -f test-suites.yml up --pull=always"
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
   sh "docker-compose -f grid.yml down"
   sh "docker-compose -f test-suites.yml down"
   archiveArtifacts artifacts: 'results/emailable-report.html', fingerprint: true
    }
   }
}