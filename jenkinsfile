node{
    
    def mavenHome = tool name : "maven3.9.6"
	
	stage('gitcheckout')
	{
	git credentialsId: '956230b7-9444-4a64-a288-317fb8a79f6c', url: 'https://github.com/nomraj-devops/maven-web-application.git'
	}
	
	stage('Maven Build')
	{
	sh "${mavenHome}/bin/mvn clean package"
	}
	
	stage('SonarQube Code Analysis')
	{
	sh "${mavenHome}/bin/mvn clean sonar:sonar"
	}
	
	stage('Deploy BuildArtifactory InTo Nexsus Server')
	{
	sh "${mavenHome}/bin/mvn clean deploy"
	}
	
	stage('Deploy BuildArtifactory InTo Nexsus Server')
	{
	sshagent(['0fbd36a5-665a-4d8a-9269-e3953e738054']) {
   sh "scp -o  StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.232.54.227:/opt/apache-tomcat-9.0.85/webapps/"
    }
	}
	
	stage('Email Verification')
	{
	 emailext body: '''pipeline is successfull....

      Regards
    Nomraj
    DevOps
    9398236773''', subject: 'pipeline is successfull....', to: 'nomraj97@gmail.com'
	}
	
	}
