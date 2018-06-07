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
    stage('Pkg') {
      steps {
        sh 'mvn package'
      }
    }
    stage('Archive') {
      steps {
        archiveArtifacts 'target/*.jar'
      }
    }
    stage('deploy') {
      steps {
        sh 'make deploy-default'
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