pipeline {
    // add your slave label name
    agent { label 'slave1'}
    tools{
        maven 'maven_repo'
    }
    stages {
        stage ('Checkout_SCM') {

            steps {
          	    
	     checkout scm
            }
        }

        stage ('Maven_Build') {

            steps {
               sh 'mvn clean package'
            }
        }
        
        stage ('Deploy_Tomcat') {

            steps {
	      sshagent(['tomcat-web-server']) {
              sh "scp -o StrictHostKeyChecking=no  target/maven-web-application.war  ec2-user@54.159.191.67:/opt/tomcat9/webapps"
	      }
         }
        }
        
    }
}
