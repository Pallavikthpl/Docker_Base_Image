pipeline {
	agent {
		dockerfile {
		label 'dockernode'
		args '-e "LICENSE=accept" -p 7801:7800 -p 7601:7600'
	}
	}
    stages{
    stage('Test'){
		     
	    steps{
	       echo "Waiting for deployment to complete before starting unit test"
                	def get = new URL("http://192.168.56.103:7801/Transformation_Map").openConnection();
			def getRC = get.getResponseCode();
			println(getRC);
			if(getRC.equals(200)) {
   			println(get.getInputStream().getText());
}}
	    }
    }}
