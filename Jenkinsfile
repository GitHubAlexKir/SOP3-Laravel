
pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                sh 'cp -r * /var/www/html'
                sh '/var/www/html/composer install'
                sh 'mv /var/www/html/.env.example /var/www/html/.env'
                sh '/var/www/html/php artisan key:generate'
            }
        }
        stage('test') {
            steps {
                sh '/var/www/html/vendor/bin/phpunit'
            }
        }
        stage('SonarQube analysis') {
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
    }
}
