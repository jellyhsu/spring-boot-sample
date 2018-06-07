pipeline {
  agent any
  stages {
    stage('checkout project') {
      steps {
        checkout scm
      }
    }
    stage('TEST') {
      steps {
        sh 'mvn cobertura:cobertura test'
      }
    }
    stage('JUnit Report') {
      parallel {
        stage('JUnit Report') {
          steps {
            junit 'target/surefire-reports/*.xml'
          }
        }
        stage('cobertura Report') {
          steps {
            cobertura(coberturaReportFile: 'target/site/cobertura/coverage.xml')
          }
        }
      }
    }
  }
  post {
    always {
      echo 'I will always say Hello again!'

    }

    success {
      echo 'success!'

    }

    failure {
      echo 'failure!'

    }

  }
}