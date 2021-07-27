pipeline
{
    agent any

stages {
    stage ("S3 download"){
        steps {
              withAWS(region: 'ap-south-1' , credentials: '74bbf8b6f36a759e6d7be9bf45e2d056248dff227bcb69c352f71fbbfb35b089') \
                 {
                      S3Download(file:'*',bucket:'s3://abhibucket00000/abhi/', path:'/home/ubuntu')
                   }
              }
       }
   }
}
