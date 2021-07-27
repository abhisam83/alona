pipeline
{
    agent any

stages {
    stage ("S3 download"){
        steps {
              withAWS(region: 'ap-south-1' , credentials: 'awsid') \
                 {
                      s3Download(file:'abhidata',bucket:'abhibucket00000', path:'abhi')
                   }
              }
       }
   }
}
