pipeline {
   agent any
	stages {
      stage('Git Checkout') {
         steps {
            git 'https://github.com/Deeps333/INGFavBank.git'
		}
	}
	stage('Build') {
		steps {
			withSonarQubeEnv('sonar') {
				sh '/opt/maven/bin/mvn clean verify sonar:sonar -Dmaven.test.skip=true'
			}
		}
	}
	stage("Quality Gate") {
            steps {
              timeout(time: 1, unit: 'MINUTES') {
                waitForQualityGate abortPipeline: true
              }
            }
          }
	stage ('Deploy') {
		steps {
			sh '/opt/maven/bin/mvn clean deploy -Dmaven.test.skip=true'
		}
	}
	stage ('Release') {
		steps {
			sh 'export JENKINS_NODE_COOKIE=dontkillme ;nohup java -jar $WORKSPACE/target/*.jar &'
		}
	}
}
}
