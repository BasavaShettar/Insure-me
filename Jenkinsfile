pipeline{
  agent any
  tools{
   maven 'MAVEN_HOME'
  }
  
  stages{
    stage('checkout git'){
      steps{
          git branch: 'main', url: 'https://github.com/BasavaShettar/Insure-me.git'
      }
    }

    stage ('maveen package')
    {
      steps{
      sh 'mvn clean install'
        }
    }

    stage ('HTML report')
    {
      steps{
publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '/var/lib/jenkins/workspace/Insurance/target/surefire-reports', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: '', useWrapperFileDirectly: true])
      }
    }
   
  
    }
}


    
