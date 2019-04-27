properties([pipelineTriggers([githubPush()])])
node('linux') {
	stage('Unit Tests') {
		sh "ant -f test.xml -v"
		junit 'reports/*.xml'
	}
	
	stage('Build') {

		sh "ant -f build.xml -v"
		
	}
	
	stage('Report') {
    	withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'jenkins-credential', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
           sh "aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins"
    }


	}
}
