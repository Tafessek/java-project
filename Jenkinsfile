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
	
	stage('Deploy') {

		withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'AWS user for Jenkins', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]){

		  sh "AWS s3 cp /workspace/javapipeline/dist/${BUILDER_NAME}-${BUILDER_NUMBER}.jar  s3://seis-665assignment10"
             }
		
	}
}
