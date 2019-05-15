
pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                sh 'php --version'
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
         stage('notify') {
            steps {
                slackSend(color: '#00FF00', message: 'BUILD PASSED')
            }
        }
    }
}
