pipeline {
	agent {
		dockerfile true
		label 'dockernode'
	}
	
    stages{
    stage('Test'){
		     
	    steps{
	        script{
	            sleep 10
	            echo "Waiting for deployment to complete before starting unit test"
                	def get = new URL("http://192.168.56.103:7801/Transformation_Map").openConnection();
			def getRC = get.getResponseCode();
			println(getRC);
			if(getRC.equals(200)) {
   			println(get.getInputStream().getText());
}}
	    }
	    }
    }}
