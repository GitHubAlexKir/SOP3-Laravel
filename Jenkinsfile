pipeline {
    agent any
    stages {
       stage("Load test Taurus") {
          steps {
              sh "bzt --help"
              bzt "load_test.yml -report"
          }
       }
    }
}

