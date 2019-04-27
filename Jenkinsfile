pipeline {
	agent any
	stages {
		stage ('Unit Tests') {
			sh "ant -f test.xml -v"
			
		}
		stage ('Results') {
			
			junit 'reports/*.xml'
		}
		
		
	}
}
