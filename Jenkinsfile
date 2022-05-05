node() {
	
	def sonarScanner = tool name: 'SonarScanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
	stage("Code Checkout"){
		checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'GitHubCreds', url: 'https://github.com/bharu11/boxfuse-sample-java-war-hello.git']]])
	}

	stage("Maven Build"){
		sh """
			ls -lart
			mvn clean install
		"""
	}

	stage("Code Review"){
		withSonarQubeEnv(credentialsId: 'SonarQubeToken') {
		//	sh "${sonarScanner}/bin/sonar-scanner"
		}
		
	}

	stage("Code Deployment"){
		//deploy adapters: [tomcat9(credentialsId: 'TomcatCreds', path: '', url: 'http://44.202.68.177:8080/')], contextPath: 'Deploy', war: 'target/*.war'
	    }
    }
	stage("Email Notification"){
		    emailext attachLog: true, attachmentsPattern: 'target/*.war', body: '''$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS:

Check console output at $BUILD_URL to view the results.''', compressLog: true, subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', to: 'bhargavi.killari11@gmail.com'
		
}
