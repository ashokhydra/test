pipeline {
	agent any
	
	stages{
		stage('Checkout Code'){
			steps{
				checkout scm
				}
			}
	
	stage('Build'){
		steps{
			bat "mvn clean install -Dmaven.test.skip=true"
		}
	}
	
	stage('Archive Artifact'){
		steps{
		archiveArtifacts artifacts:'target/*.war'
		}
	}
	
	stage('deployment'){
		steps{
		//deploy adapters: [tomcat9(credentialsId: 'TomcatCreds' path: '', url: 'http://http://172.167.243.18/:8080/')], contextPath: 'counterwebapp', war: 'target/*.war'
		deploy adapters: [tomcat9(url: 'http://172.174.230.44:8080/', 
                              credentialsId: 'TomcatCreds')], 
                     war: 'target/*.war',
                     contextPath: 'app'
		}
		
	}
	
	stage('Notification'){
		steps{
		emailext(
			subject: "Job Completed",
			body: "Jenkins pipeline job for maven build job completed",
			to: "sudheer.baraker@gmail.com"
		)
		}
	}
	}
}
