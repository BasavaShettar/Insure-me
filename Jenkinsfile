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
        stage('docker file and image')
          {
            steps{
                 sh 'docker build -t basavarajshettar/insure-app:1.0 .'
            }
          }
stage('Docker image push') {
    steps {
    withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
          sh ' docker login -u basavarajshettar -p ${dockerhubpwd}'
}
      sh 'docker push basavarajshettar/insure-app:1.0'
      
            }
        }
    stage('Deploy on server'){
  steps{
ansiblePlaybook credentialsId: 'Ansible_Server', disableHostKeyChecking: true, installation: 'Ansible', inventory: 'home/basava/host', playbook: 'ansible-playbook.yml'
  }

  
}

    }
}


    
