pipeline {
  agent any
  stages {
    stage('cleanup') {
      steps {
        dir(path: 'reports') {
          deleteDir()
        }
        
      }
    }
    stage('build: docker image') {
      steps {
        script {
          date = sh(returnStdout: true, script: 'date +%Y%m%d-%H%M%S').trim()
        }
        
      }
    }
    stage('test') {
      steps {
        parallel(
          "test: app backend": {
            sh '"echo ${date}"'
            
          },
          "code analysis: php": {
            sh 'echo ${reports_path}'
            
          }
        )
      }
    }
    stage('push: docker image') {
      steps {
        sh '"echo push docker image"'
      }
    }
  }
  environment {
    docker_service_name = 'web-eqr'
    reports_path = "${WORKSPACE}/reports"
  }
}