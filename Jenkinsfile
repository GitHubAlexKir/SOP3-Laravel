
pipeline {
    agent any
    stages {
       stage("Load test Taurus") {
          steps {
              script {
                sh 'pip install bzt'
                sh 'bzt load_test.yml -report'
              }
          }
       }
    }
}
