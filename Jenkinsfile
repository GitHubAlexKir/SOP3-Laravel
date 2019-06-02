
pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                sh "docker build -t laravel-app:B${BUILD_NUMBER} -f Dockerfile ."
            }
        }
        stage('SonarQube analysis + test') {
           steps {
               script {
                  def scannerHome = tool 'laravelScanner'
                  withSonarQubeEnv('AlexLarsSonarqube') {
                      sh "${scannerHome}/bin/sonar-scanner"
                  }
                  sh 'echo this is needed because of slowness of seclab'
                  def time = '10'
                  sleep time.toInteger()
               }
            }
        }
        stage("Quality Gate 1") {
          steps {
                waitForQualityGate abortPipeline: true
            }
        }
        stage("Deploy") {
          steps {
             sh "chmod -R 777 storage"
             sh "docker-compose -f docker-compose.yml up -d --force-recreate"
          }
       }
    }
}
