pipeline {
    agent any
    environment { 
        docker_service_name = 'web-eqr'
        reports_path = "${WORKSPACE}/reports"
        //date = 'temp_var'
    }
    
    stages {
        stage('cleanup') {
            steps {
                dir('reports') {
                    deleteDir()
                }
            }
        }
        stage('build: docker image') {
            steps {
                script {
                    date = sh(returnStdout: true, script: 'date +%Y%m%d-%H%M%S').trim()
            
                    //container = docker.build("${docker_service_name}:${date}")
                }
            }
        }
        stage('test') {
            steps {
                parallel (
                    'test: app backend': {
                        sh "echo ${date}"    
                    },
                    'code analysis: php': {
                        sh 'echo ${reports_path}'
                    }
                )
            }
        }
    }
}
