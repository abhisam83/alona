pipeline
{
    agent any

stages {
    stage ("S3 download"){
        steps {
                withAWS(region: 'ap-south-1' , credentials: 'awsid') \
                 {
                      s3Download(file:'abhidata',bucket:'abhibucket00000', path:'gold/')
                      s3Download(file:'abhidata1',bucket:'abhibucket00000', path:'bronze/')
                   }
              }
       }
    stage (" File Segregation ") {
        
        steps {
          sh 'mkdir -p internal && mkdir -p external'
          sh 'cp abhidata/gold/ external/'
          sh 'cp abhidata1/bronze/ internal/'  
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
