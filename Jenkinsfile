
pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                sh "docker build -t laravel-app:B${BUILD_NUMBER} -f Dockerfile ."
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
             sh "rm -rf storage/logs/*"
             sh "rm -rf storage/framework/views/*"
             sh "rm -rf storage/framework/sessions/*"
             sh "chmod -R 777 storage"
             sshPublisher(publishers: [sshPublisherDesc(configName: 'DEV', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'docker-compose -f docker/docker-compose.yml up -d --force-recreate', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '/docker', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '*')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
          }
       }
    }
}
