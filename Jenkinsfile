pipeline {
  agent {
    node {
      label 'docker'
    }
  }
  parameters {
             string(name: 'COMPONENT', defaultValue: '', description: 'Which component')
             string(name: 'ENV', defaultValue: 'prod', description: 'Which environment')
             string(name: 'APP_VERSION', defaultValue: '', description: 'Which version')
     }

  stages{
    stage('Helm Chart Deploy'){
      steps{
      sh 'aws eks update-kubeconfig --name ${ENV}-eks'
      sh 'heml upgrade -i ${component} roboshop'
       }

    }
  }
}
