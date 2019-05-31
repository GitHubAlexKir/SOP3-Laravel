
pipeline {
    agent any
    parameters {
        booleanParam(name: 'deploy', defaultValue: true, description: 'Deploy code to Environment')

        choice(name: 'environment', choices: ['DEV', 'PROD', 'ACC'], description: 'Environment to deploy to')
    }
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
              sh "rm -rf /var/www/html/${params.ENVIRONMENT}"
              sh "mkdir /var/www/html/${params.ENVIRONMENT}"
              sh "cp -r * /var/www/html/${params.ENVIRONMENT}"
              sh "cp -r * /var/www/html/${params.ENVIRONMENT}"
              sh "cp .env /var/www/html/${params.ENVIRONMENT}/.env"
              sh "rm /var/www/html/${params.ENVIRONMENT}/storage/logs/*"
          }
        }
    }
}
