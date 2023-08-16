
pipeline {
    agent any
    tools {
	    maven 'maven-jenkins'
    }
    stages {
        stage('MAVEN BUILD'){
            steps{
                sh 'mvn clean package'
		sh 'mv target/*.war target/tomcat-app.war'
            }
        }
    	post {
            success { 
            	echo "This pipeline is successfull!"
            }
    	    unsuccessful {
            	echo "ISSUE!!!"
            }
    }
}
