pipeline {
	agent {
		dockerfile true{
		label 'dockernode'
		args '-e "LICENSE=accept" -p 7801:7800 -p 7601:7600'
	}
	}
    stages{
    stage('Test'){
		     
	    steps{
	        echo "Successful run"
}}
	    }

