pipeline 
{
    agent any

    environment {
        RC_FOLDER = 'abhilashsam'
        
    }
stages {
    stage ("S3 download"){
        steps {
            script {
                Date date = new Date()
                env.RC_DATE = date.format ("yyyy-MM-dd_hh-mm")
            }
                withAWS(region: 'ap-south-1' , credentials: 'awsid') \
                 {
                     s3Download(file:"${RC_FOLDER}-${RC_DATE}/",bucket:'abhibucket00000', path:'RC_Folder/')
                      
                 }
              }
       }
    stage (" File Segregation ") {
                
        steps {
            script {
                Date date = new Date()
                env.RC_DATE = date.format ("yyyy-MM-dd_hh-mm")
            }
          sh 'mkdir -p internal10 && mkdir -p external10'
            sh 'cp -r ${RC_FOLDER}-${RC_DATE}/RC_Folder/gold/ external10/ && cp -r ${RC_FOLDER}-${RC_DATE}/RC_Folder/bronze/ internal10/'
          }
    
    }
    stage ("S3 Upload "){
       steps {
                withAWS(region: 'ap-south-1' , credentials: 'awsid') \
                  {
                      s3Upload(
                          bucket:'nymi-release1', file: 'external10/', path:'external/')
                      s3Upload(
                          bucket:'nymi-release1', file: 'internal10/', path:'internal/')
                   }
            }
    
      
    }
  }

}    
