pipeline {
        agent any
        stages {
	     stage (“Checkout”) {
             steps {
             git 'https://github.com/krishnakumar6893/maven_demo'             
	     }
	     }

	     stage (“Maven build”) {
             steps {
             sh 'mvn clean install'
	     }
	     }

             stage (“JUnit”) {
             steps {
             junit '**/gameoflife-web/target/surefire-reports/*.xml, **/gameoflife-core/target/easyb/*.xml, **/gameoflife-core/target/surefire-reports/*.xml'
	     }
	     }

             stage (“Building docker image”) {
             steps {
             sh label: '', script: 'docker build -t tomcat .'
	     }
	     }
	}
}
