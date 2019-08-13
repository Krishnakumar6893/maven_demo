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

             stage (“Reports”) {
             steps {
             junit '**/gameoflife-web/target/surefire-reports/*.xml, **/gameoflife-core/target/easyb/*.xml, **/gameoflife-core/target/surefire-reports/*.xml'
	     }
	     }
	}
}
