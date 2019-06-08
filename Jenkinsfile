pipeline {
    agent { docker 'blazemeter/taurus' }
    stages {
       stage("Load test Taurus") {
          steps {
              sh "bzt load_test.yml -report"
          }
       }
    }
}

