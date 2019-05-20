
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
                slackSend(color: '#00FF00', baseUrl: 'https://fontys-space.slack.com/services/hooks/jenkins-ci/', teamDomain: 'fontys-space', channel: 'general', tokenCredentialId:'DZqE3UJMJD0ttkWxt779cglW',message: 'BUILD PASSED')
            }
        }
    }
}
