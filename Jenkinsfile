pipeline
{
    agent any

stages {
    stage ("S3 download"){
        steps {
              withAWS(region: 'ap-south-1' , credentials: 'awsid') \
                 {
                      S3Download(file:'*',bucket:'s3://abhibucket00000/abhi/', path:'/home/ubuntu')
                   }
              }
       }
   }
}
