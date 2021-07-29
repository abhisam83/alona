pipeline {
		agent any
		
			environment {
			
			RC 		= 'RC_folder'       		//Directory name in S3 bucket nymi-rc, Eg: Value of "${RC}-${RC_DATE}/" from RC Packaging Project
			RELEASE 	= 'firmware '    		//Release directory name, Eg: firmware, SDCT, sdk
			RC_FOLDER 	= 's3downloader'  				//Download directory in workspace, Eg: <any name>
	} 
	
	stages {

		stage ("S3 download"){
	
			steps {
		
				withAWS(region: 'ap-south-1' , credentials: 'awsid') \
                 {
                     s3Download(
					 file: "abhi-${RC_FOLDER}/", bucket:'nymi-rc1', path:"${RC}/")
                      
                 }
              }
			}
		stage (" File Segregation ") {
                
			steps {
            
				script {
             			
				def services = ['firmware', 'SDCT']
                    		for (int i = 0; i < services.size(); ++i) {
					def a = fileExists "abhi-${RC_FOLDER}/${RC}/${services[i]}"
						//sh 'mkdir -p external && mkdir -p internal'
					if (a) {
					sh 'echo "Testing the ${services[i]}"'
					}
					else {
					sh 'echo "Not Valid"'
					}
				}
				}
			}
		}
					
						
			
				/* sh 'echo "Downloaded Completed"'
				def firmware_gold = fileExists "abhi-${RC_FOLDER}/${RC}/firmware/gold"
				
				if (firmware_gold) {
    				sh 'mkdir -p external && mkdir -p internal'
				
				} 
				elif {
				def firmware_bronze = fileExists "abhi-${RC_FOLDER}/${RC}/firmware/bronze"
    				sh 'mkdir -p internal'	
					}		
				//firmware gold
				//sh 'cd abhi-${RC_FOLDER}/${RC}/firmware/			
				//sh 'mkdir -p abhi-${RC_FOLDER}/${RC}/firmware/abhilashalona'
				
					}
				}
			}
			*/
		
		stage ("Promote Release "){
            when {
				branch 'release-*'
			}
			steps {	   
		        
				withAWS(region: 'ap-south-1' , credentials: 'awsid') \
                  {
                      s3Upload(
                          acl: 'Private', bucket:'nymi-release1', file: 'release-${RELEASE}', path:'release-${RELEASE}')
                      
					  }
				}
    
      
			}
		}

	
  
  
}    
