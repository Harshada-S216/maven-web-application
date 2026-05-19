pipeline{
        
		  agent any
		  
		  tools {
		    maven 'maven3'
		  }
		  
    stages{
	
	 stage('gitCheckOut'){
	  steps{
	  git branch: 'main', url: 'https://github.com/Harshada-S216/maven-web-application.git'
	  }
	 }
	
 stage('mavenBuild'){
  steps{
  sh "mvn clean package"
  }
 }
 
 stage('sonarAnalysis'){
  steps{
  sh "mvn sonar:sonar"
  }
 }
	
    stage('nexusUpload'){
     steps{
     sh "mvn deploy"
     }
    }
	
    stage('tomcatHosting'){
     steps{
      sshagent(['tomcat-key']) {
        sh """
  	  scp -o StrictHostKeyChecking=no target/maven-web-application.war ubuntu@3.111.34.93:/opt/tomcat/webapps/
  	  """
    }
     }
    }
	
	} //stages closing
}
