pipeline {
		agent any
		
			environment {
			
			RC 		= 'RC_folder'       		
			RELEASE 	= 'firmware '    		
			 				
	} 
	
	stages {

		Stage("Copying source S3 to target S3") {
			step {
				withAWS(region: 'ap-south-1' , credentials: 'awsid')
				s3copy(
					fromBucket: 'nymi-rc1', fromPath: "${RC}/", toBucket: 'nymi-release1', toPath: release-"${RELEASE}")
			

	}
}
