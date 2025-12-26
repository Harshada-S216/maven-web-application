
pipeline {
    agent any

    tools {
        maven 'Maven_3.9.7'
    }

    stages {

        stage('Checkout Code to Jenkins from GitHub') {
            steps {
                git branch: 'dev',
                url: 'https://github.com/sanket0101/maven-web-application.git'
            }
        }
    }
}


