pipeline {
  agent any
  stages {
    stage('test') {
      parallel {
        stage('test') {
          steps {
            sh 'gcgfc'
          }
        }

        stage('tools') {
          steps {
            tool(name: 'sfdx', type: 'c')
          }
        }

      }
    }

    stage('deploy') {
      steps {
        sh 'hh'
      }
    }

  }
}