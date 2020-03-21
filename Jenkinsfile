pipeline {
   agent any
	stages {
      stage('Git Checkout') {
         steps {
            checkout([$class: 'GitSCM', branches: [[name: '*/mybranch']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/Deeps333/INGFavBank.git']]])
		}
	}
	stage ('Build')
	   
	    {steps{
                sh '/usr/share/maven/bin/mvn clean package -Dmaven.test.skip=true'
	    }    }
       
	}}
      
