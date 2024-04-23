pipeline{
agent any
    stages{

    stage('Run Selenium Grid')
    {
        steps{
        script
        {
        bat "docker-compose up"
        }
      }
    }

    stage('Shut Down Grid')
    {
        steps{
        bat "docker-compose down"
    }
    }

    }
}