pipeline {
    agent any

    tools {
        maven 'maven9.9'
        git 'Default'
    }

    stages {
        stage('gitCheckout') {
            steps {
                git branch: 'main', url: 'https://github.com/Harshada-S216/maven-web-application.git'
            }
        }

        stage('mavenBuild') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('sonarAnalysis') {
            steps {
                sh 'mvn sonar:sonar'
            }
        }
        stage('NexusDeploy'){
            steps{
               sh "mvn deploy"
              }
           }

         stage('tomcatDeploy'){
            steps{
            sshagent(['Tomcat key pem']) {
              sh """
      	  scp -o StrictHostKeyChecking=no target/maven-web-application.war ubuntu@15.206.90.54:/opt/apache-tomcat-9.0.106/webapps/
        	  """
                 }
              }
            }
        
          }
         post {
          success {
              slackSend (
                  color: 'good', // green
                  message: "✅ *Build Success* - Job: ${env.JOB_NAME}, Build: #${env.BUILD_NUMBER}\n<${env.BUILD_URL}|Click here to view details>"
              )
          }
          failure {
              slackSend (
                  color: 'danger', // red
                  message: "❌ *Build Failed* - Job: ${env.JOB_NAME}, Build: #${env.BUILD_NUMBER}\n<${env.BUILD_URL}|Click here to view details>"
              )
          }
          unstable {
              slackSend (
                  color: 'warning', // yellow
                  message: "⚠️ *Build Unstable* - Job: ${env.JOB_NAME}, Build: #${env.BUILD_NUMBER}\n<${env.BUILD_URL}|Click here to view details>"
              )
          }
      }	  
 }

