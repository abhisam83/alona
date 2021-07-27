pipeline {
    agent  {any}

    enironment {
        RC_FOLDER = 'abhi'
    }
stages {
    stage ("S3 download"){
        steps {
                withAWS(region: 'ap-south-1' , credentials: 'awsid') \
                 {
                     s3Download(file:'${RC_FOLDER}',bucket:'abhibucket00000', path:'RC_Folder/')
                      
                 }
              }
       }
    stage (" File Segregation ") {
        
        steps {
          sh 'mkdir -p internal && mkdir -p external'
            sh 'cp -r ${RC_FOLDER}/RC_Folder/gold/ external/ && cp -r ${RC_FOLDER}/RC_Folder/bronze/ internal/'
          }
    
    }
    stage ("S3 Upload "){
       steps {
                withAWS(region: 'ap-south-1' , credentials: 'awsid') \
                  {
                      s3Upload(
                          bucket:'adambucket00000', file: 'external/', path:'external/')
                      s3Upload(
                          bucket:'adambucket00000', file: 'internal/', path:'internal/')
                   }
            }
    
      
    }
  }

}    
