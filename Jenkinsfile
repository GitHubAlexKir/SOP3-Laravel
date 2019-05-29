
pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                sh '/var/www/html/composer install'
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
                  def time = '5'
                  sleep time.toInteger()
               }
            }
        }
        stage("Quality Gate 1") {
            steps {
                waitForQualityGate abortPipeline: true
            }
        }
        stage('Deployment') {
            steps {
                sh 'cp -r * /var/www/html'
                sh 'cp .env /var/www/html/.env'
            }
       }
    }
}
