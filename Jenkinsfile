pipeline {
		agent any
		
	stages {
		stage("Copying source S3 to target S3") {
			step {
			 	withAWS(region: 'ap-south-1' , credentials: 'awsid')
				aws s3 cp s3://nymi-rc1/RC_Folder s3://nymi-release1/ --recursive
			}
		}
	}
}
