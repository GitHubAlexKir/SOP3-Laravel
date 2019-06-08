node  {
       stage("Load test Taurus") {
            BlazeMeterTest: {
                dir ('SOP3-Laravel'){
                 sh 'bzt load_test.yml'  
                }
            }
       }
  }

