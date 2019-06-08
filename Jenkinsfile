pipeline {
    agent any
    stages {
       stage("Load test Taurus") {
          steps {
              sh "taurus-venv/bin/bzt load_test.yml -report"
          }
       }
    }
}

