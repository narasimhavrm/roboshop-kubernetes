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
    stage('Clone app repo'){
      steps{
        dir('APP'){
          git branch: 'main', url: 'https://www.github.com/narasimhavrm/${COMPONENT}'
        }
      }
    }
    stage('Helm Chart Deploy'){
      steps{
      sh 'aws eks update-kubeconfig --name ${ENV}-eks'
      sh 'helm upgrade -i ${COMPONENT} roboshop -f APP/helm.yml --set image.tag=${APP_VERSION}'
       }

    }
  }

  post {
    always {
      cleanWs()
    }
  }
}
