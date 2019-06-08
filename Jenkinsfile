pipeline {
    agent { docker 'blazemeter/taurus' }
    stages {
       stage("Load test Taurus") {
          steps {
              bzt "load_test.yml -report"
          }
       }
    }
}

