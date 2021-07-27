pipeline 
{
    agent any

    environment {
        RC_FOLDER = 'abhi'
        Date date = 'new Date()'
        RC_DATE = date.format ("yyyy-MM-dd_hh-mm")
    }
stages {
    stage ("S3 download"){
        steps {
                withAWS(region: 'ap-south-1' , credentials: 'awsid') \
                 {
                     s3Download(file:"${RC_FOLDER}-${RC_DATE}/",bucket:'abhibucket00000', path:'RC_Folder/')
                      
                 }
              }
       }
    stage (" File Segregation ") {
        
        steps {
          sh 'mkdir -p internal && mkdir -p external'
            sh 'cp -r ${RC_FOLDER}-${RC_DATE}/RC_Folder/gold/ external/ && cp -r ${RC_FOLDER}/RC_Folder/bronze/ internal/'
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
