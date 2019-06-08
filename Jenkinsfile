pipeline {
    agent any
    stages {
       stage("Load test Taurus") {
          steps {
              bzt "load_test.yml -report"
          }
       }
    }
}

