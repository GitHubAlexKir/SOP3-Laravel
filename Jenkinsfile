
pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                sh "docker build -t laravel-app:B${BUILD_NUMBER} -f Dockerfile ."
            }
        }
        stage("Deploy") {
          steps {
             sh "docker-compose -f docker-compose.yml up --force-recreate"
          }
        }
    }
}
