
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
        stage('test') {
            steps {
                sh 'vendor/bin/phpunit'
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
        stage('Deployment') {
            steps {
                sh 'ls -al'
                sh 'cp -r * /var/www/html'
                sh 'ls -al /var/www/html'
                sh 'cat .env' 
                sh 'cat /vat/www/html/.env'
            }
        }
    }
}
