
pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                sh 'composer install'
                sh 'mv .env.example .env'
                sh 'php artisan key:generate'
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
             sh "docker-compose -f docker-compose.yml up --force-recreate --abort-on-container-exit"
          }
        }
    }
}
