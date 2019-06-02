
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
        stage("Deploy") {
          steps {
             sh "docker-compose -f docker-compose.yml up --force-recreate"
          }
        }
    }
}
