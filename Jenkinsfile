pipeline {
	agent {Dockerfile true}
	environment
	{
	ant_build = "C:\\Users\\PallaviKathpalia\\IBM\\IIBT10\\workspace_New\\ESPFlow\\Build\\build.xml"
	registry = "pallavikthpl/iibmq_poc1"
  registryCredential = 'dockerhub'
	dockerImage = ''
	}
    stages {
	    
        stage('Checkout') { 
            
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/Pallavikthpl/Docker_Base_Image.git']]])
            }
        }
        
        
	  stage('Build') {
		steps
		{
		withAnt(installation: 'apache-ant-1.9.14', jdk: 'jdk-12.0.1'){
		// some block
		bat "ant -f ${ant_build}"
		}
		}
	}
	    stage('upload') {
		steps {
		script {
			def server = Artifactory.server 'JfrogArtifactory'
			def uploadSpec = """{
			"files": [{
			"pattern": "C:/Users/PallaviKathpalia/JenkinsUCD/",
			"target": "jenkins"
			}]
			}"""
 
			server.upload(uploadSpec)
			}
		}
		}
	    stage('Call Image Build Pipeline'){
	    steps{
		    build 'Docker_Image_Pipeline'
	    }
	    }
            }
}
