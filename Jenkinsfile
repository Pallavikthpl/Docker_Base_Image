pipeline {
	agent none
	environment
	{
	registry = "pallavikthpl/iibmq_poc1"
        registryCredential = 'dockerhub'
	dockerImage = ''
	}
    stages {
	    
        stage('Checkout Dockerfile') { 
		agent{label 'dockernode'}
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/dockerfile']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'multibranch github Id', url: 'https://github.com/Pallavikthpl/Docker_Base_Image.git']]])
            }
        }
         
	  
	    stage('Build Docker Image'){
		     agent{label 'dockernode'}
	    steps{
		    script{
		    docker.build("aceappimage:${env.BUILD_ID}", "/home/pallavi/VM2/workspace/Docker_Image_Pipeline@2")
	    }
	    }
	    }
	    
	     stage('Run Container'){
		     agent{label 'dockernode'}
		     steps{
			     docker{
			     image 'aceappimage:${env.BUILD_ID}'
			     args '-e "LICENSE=accept" -p 78${env.BUILD_ID}:7800 76${env.BUILD_ID}:7600'
		    
			     }	    
	    }
	    }
	    
	    stage('Deploy Image') {
  		steps{    
			script {
      			docker.withRegistry( '', registryCredential ) {
        		dockerImage.push()
      }
    }
  }
}
            }
}
