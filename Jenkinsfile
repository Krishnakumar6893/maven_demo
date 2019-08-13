pipeline {
        agent any
        stages {
	     stage (“Checkout”) {
             steps {
             git 'https://github.com/krishnakumar6893/maven_demo'             
	     }
	     }
	}

        stages {
	     stage (“Build”) {
             steps {
             sh 'mvn clean install'
	     }
	     }
	}
}
