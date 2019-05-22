
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
        stage('SonarQube analysis') {
            steps {
                // requires SonarQube Scanner 2.8+
                def scannerHome = tool 'SonarQube Scanner 2.8';
                withSonarQubeEnv('My SonarQube Server') {
                     sh "${scannerHome}/bin/sonar-scanner"
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
