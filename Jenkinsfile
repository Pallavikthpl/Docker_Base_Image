pipeline {
	agent {label 'dockernode'}
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
        stage('Download Bar file') {
		  agent{label 'dockernode'}
		steps
		{
		script {
			@NonCPS
			def server = Artifactory.server 'JfrogArtifactory'
			def downloadSpec = """{
			"files": [{
			"pattern": "jenkins/*.bar",
			"target": "/"
			}]
			}"""
 
			server.download(downloadSpec)
			}
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
