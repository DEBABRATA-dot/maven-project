pipeline{
 tools{
        jdk 'JAVA_HOME'
        maven 'M2_HOME'
    }
     agent any
	  
	  stages{
	  
	  stage("checkout"){
	   steps{
	   git 'https://github.com/DEBABRATA-dot/maven-project.git'
	   }
	                  }
	
	   stage("compile"){
	    steps{
		 sh 'mvn compile'
		}
		}
       stage("test"){
	    steps{
		 sh 'mvn test'
		}
		}
       stage("package"){
	    steps{
		 sh 'mvn clean package'
                 sh "mv target/*.jar target/myweb.war"

		}
		}
   stage("deploy"){
	   steps{

      sshagent(['Debabrata']) {

	        sh """
                 
            scp -o StrictHostKeyChecking=no target/myweb.jar ec2-user@15.207.16.254:/home/ec2-user/tomcat8/webapps/

              ssh ec2-user@15.207.16.254 /home/ec2-user/tomcat8/bin/shutdown.sh
               ssh ec2-user@15.207.16.254 /home/ec2-user/tomcat8/bin/startup.sh
            
          
          """

}   
		}
		  
	  }
	  }
	  }

