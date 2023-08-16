
pipeline {
    agent any
    tools {
	    maven 'maven-jenkins'
    }
    stages {
        stage('MAVEN BUILD'){
            steps {
                sh 'mvn clean package'
		sh 'mv target/*.war target/tomcat-app.war'
            }
        }
	stage('DEPLOY'){
            steps {
                sshagent(['jenkins-agent-creds']) {
                    sh '''
                
                    scp -o StrictHostKeyChecking=no target/tomcat-app.war ec2-user@172.31.27.181:/opt/tomcat9/webapps
                    ssh ec2-user@172.31.27.181 /opt/tomcat9/bin/shutdown.sh
                    ssh ec2-user@172.31.27.181 /opt/tomcat9/bin/startup.sh
                
                    '''
            }
        }  
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
