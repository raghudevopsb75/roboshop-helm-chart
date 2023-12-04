pipeline {

  agent any

  options {
    ansiColor('xterm')
  }

  parameters {
    choice(name: 'ENV', choices: ['dev', 'prod'], description: 'Choose Environment')
    string(name: 'APP_NAME', defaultValue: '', description: 'Choose AppName')
    string(name: 'VERSION', defaultValue: '', description: 'Version to Deploy')
  }

  stages {

    stage('Deployment') {
      steps {
         dir('APP') {
           git branch: 'main', url: "https://github.com/raghudevopsb75/${APP_NAME}"
         }
        dir('HELM') {
          git branch: 'main', url: "https://github.com/raghudevopsb75/roboshop-helm-chart"
          sh 'helm upgrade -i ${APP_NAME} . -f ${WORKSPACE}/APP/helm/${ENV}.yaml --set appVersion=${VERSION}'
        }

      }
    }

  }

  post {
    always {
      cleanWs()
    }
  }

}