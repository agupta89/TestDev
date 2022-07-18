env.environment ="main"
env.browserName= "firefox"

pipeline {
agent any 

stages {
        stage('Checkout Code..') {
		when {
                   anyOf { 
		   branch 'main'; branch 'stg' ; 
		   }
	           beforeAgent true
		   }
                   steps {
		   echo 'Hello World'
                   script {			    	
                   if ("${env.GIT_BRANCH}" == "main") {
                   env.environment = "dev"
		    } else if("${env.GIT_BRANCH}" == "stg"){
                   env.environment = "stg"
		    } else {
                    env.environment = "false"
                   }
		    echo env.environment
		    checkout([$class: 'GitSCM', branches: [[name: 'master']],doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/agupta89/TestQA.git']]])
                    
                }
		  		
            }
}

    stage('Checkout Testing Code') {
           steps {     
           wrap([$class: 'Xvfb', additionalOptions: '', assignedLabels: '', autoDisplayName: true, debug: false, shutdownWithBuild: true ,displayNameOffset: 1,installationName: 'Xvfb', parallelBuild: true, screen: '1600x1280x24', timeout: 60])
           {
                sh ' mvn -f pom.xml clean install'
		
            }
        }
    }

      stage('Publish Html Report') {
            steps {
                echo 'Extend Report'       
        }

        }   
}
}
