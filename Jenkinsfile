pipeline {
        agent any
        stages {

	     stage (“Build”) {
             steps {
             sh 'mvn clean install'
	     }
	     }

             stage (“JUnit”) {
             steps {
             junit '**/gameoflife-web/target/surefire-reports/*.xml, **/gameoflife-core/target/easyb/*.xml, **/gameoflife-core/target/surefire-reports/*.xml'
	     }
	     }
		
	     stage ("Sonarqube") {
             environment {
             scannerHome = tool 'SonarQubeScanner'
             }
             
             steps {
             withSonarQubeEnv('sonarqube') {
             sh "${scannerHome}/bin/sonar-scanner"
             }
             }
             }
		
             mail (to: 'krishnakumar.santhanam@imaginea.com',
             subject: "Job '${env.JOB_NAME}' (${env.BUILD_NUMBER}) is waiting for input",
             body: "Please go to ${env.BUILD_URL}.");
             input 'Ready to go?';   

             stage (“Deploy”) {
             steps {
             sh label: '', script: '''docker build -t tomcat .
             docker run -d -p 84:8080 --name container tomcat:latest'''
	     }
	     }
	}
}
