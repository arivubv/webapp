pipeline {
 agent any
	tools {
		maven 'Maven'
	}
	stages {
		stage ('initialize'){
			steps {
			sh '''
         		echo "PATH = $(PATH)"
         		echo "M2_HOME = ${M2_HOME}"
        		'''
			}
		
		}
		stage ('Gitcheckout'){
			steps{
			git 'https://github.com/arivubv/webapp.git'
			}
		}
		stage ('build'){
			steps {
			sh 'mvn clean package'
			}
		}
		
		stage("Copy the war file to tomcat server"){
	    steps{
	        sshagent(['tomcatconnect']) {
            sh 'scp -o StrictHostKeyChecking=no target/*.war root@10.10.10.6:/root/tomcat/webapps'
		}
	    }
		}
	}
}
