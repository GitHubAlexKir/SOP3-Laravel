pipeline {
    agent any
    
       stage("Load test Taurus") {
          steps {
              bzt "load_test.yml -report"
          }
       }
    }
}
