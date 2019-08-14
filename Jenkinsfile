pipeline {
        agent any
        stages {
	     stage (“Checkout”) {
             steps {
             git 'https://github.com/krishnakumar6893/maven_demo'             
	     }
	     }

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
             timeout(time: 10, unit: 'MINUTES') {
             waitForQualityGate abortPipeline: true
             }
             }
             }

             stage (“Deploy”) {
             steps {
             sh label: '', script: '''docker build -t tomcat .
             docker run -d -p 84:8080 --name container tomcat:latest'''
	     }
	     }
	}
}
