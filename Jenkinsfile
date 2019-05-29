
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
        stage('Deployment') {
            steps {
                sh 'cp -r * /var/www/html'
                sh 'cp .env /var/www/html/.env'
                sh 'rm /var/www/html/storage/logs/*'
            }
       }
    }
}
