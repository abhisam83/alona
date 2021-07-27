pipeline
{
    agent any

stages {
    stage ("S3 download"){
        steps {
                withAWS(region: 'ap-south-1' , credentials: 'awsid') \
                 {
                      s3Download(file:'abhidata',bucket:'abhibucket00000', path:'abhi/')
                   }
              }
       }
    stage (" File Segregation ") {
        
        steps {
          sh 'mkdir -p internal && mkdir -p external'
          sh 'cp /var/jenkins_home/workspace/s3tos3/abhidata/gold/ /external/'
          sh 'cp /var/jenkins_home/workspace/s3tos3/abhidata/bronze/ /internal/'  
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
