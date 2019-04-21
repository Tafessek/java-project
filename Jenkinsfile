properties([pipelineTriggers([githubPush()])])
node('linux') {
	stage('Build') {
		git 'https://github.com/Tafessek/java-project.git'
		sh "ant -f build.xml -v"
	}

	stage('Unit Tests') {
		sh "ant -f test.xml -v"
	}
	
	

	stage('Report') {
		withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'AWScredential', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
			sh "aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins"
		}

	}
}
