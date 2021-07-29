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
             			
				sh '''
			
			//firmware gold
				cd "abhi-${RC_FOLDER}/${RC}/firmware"
							
				if [-d "gold" ]
				then
					mkdir -p release-${RELEASE}/firmware/external
					cp -r ${RC_FOLDER}/${RC}/firmware/gold/"*" release-${RELEASE}/firmware/external/
				
			//firmware bronze			
			
				elif [ -d "${RC_FOLDER}-${RC}/firmware/bronze/"]
				then 
					mkdir -p release-${RELEASE}/firmware/internal
					cp -r ${RC_FOLDER}-${RC}/firmware/bronze/"*" release-${RELEASE}/firmware/internal/
			
						
			//NBA gold
			
				elif [-d "${RC_FOLDER}/${RC}/NBA/gold/"]
				then
					mkdir -p release-${RELEASE}/NBA/external
					cp -r ${RC_FOLDER}/${RC}/NBA/gold/"*" release-${RELEASE}/NBA/external/
				
			//NBA bronze/				
			
				elif [-d "${RC_FOLDER}-${RC}/NBA/bronze/"]
				then 
					mkdir -p release-${RELEASE}/NBA/internal
					cp -r ${RC_FOLDER}-${RC}/NBA/bronze/"*" release-${RELEASE}/NBA/internal/
			
			//SDK gold
			
				elif [-d "${RC_FOLDER}/${RC}/sdk/gold/"]
				then
					mkdir -p release-${RELEASE}/sdk/external
					cp -r ${RC_FOLDER}/${RC}/sdk/gold/"*" release-${RELEASE}/sdk/external/
			
			//SDK bronze		
			
				elif [-d "${RC_FOLDER}-${RC}/sdk/bronze/"]
				then 
					mkdir -p release-${RELEASE}/sdk/internal
					cp -r ${RC_FOLDER}-${RC}/sdk/bronze/"*" release-${RELEASE}/sdk/internal/
			
			
			//OpenSC gold
			
				elif [-d "${RC_FOLDER}/${RC}/OpenSC/gold/"]
				then
					mkdir -p release-${RELEASE}/OpenSC/external
					cp -r ${RC_FOLDER}/${RC}/OpenSC/gold/"*" release-${RELEASE}/OpenSC/external/
			
			//OpenSC bronze		
			
				elif [-d "${RC_FOLDER}-${RC}/OpenSC/bronze/"]
				then 
					mkdir -p release-${RELEASE}/OpenSC/internal
					cp -r ${RC_FOLDER}-${RC}/OpenSC/bronze/"*" release-${RELEASE}/OpenSC/internal/
			
			//SDCT gold
			
				elif [-d "${RC_FOLDER}/${RC}/SDCT/gold/"]
				then
					mkdir -p release-${RELEASE}/SDCT/external
					cp -r ${RC_FOLDER}/${RC}/SDCT/gold/"*" release-${RELEASE}/SDCT/external/
			
			//SDCT bronze		
			
				elif [-d "${RC_FOLDER}-${RC}/SDCT/bronze/"]
				then 
					mkdir -p release-${RELEASE}/SDCT/internal
					cp -r ${RC_FOLDER}-${RC}/SDCT/bronze release-${RELEASE}/SDCT/internal/
			
				else
					cp -r ${RC_FOLDER}-${RC}/ release-${RELEASE}/
			
				fi
			
				'''
						
					}
				}
			}
			
		
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
