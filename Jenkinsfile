pipeline {
   agent any

   tools {
      // Install the Maven version configured as "M3" and add it to the path.
      maven "M3"
   }
   
   		

   stages {
       
      
		
      stage('Build') {
         steps {
             
            checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'githubcred', url: 'https://github.com/chakri950/cicd.git']]])
             
            // Get some code from a GitHub repository
            //git 'https://github.com/chakri950/tools.git'

            // Run Maven on a Unix agent.
            //sh "mvn -Dmaven.test.failure.ignore=true clean package"

            // To run Maven on a Windows agent, use
            bat "mvn -Dmaven.test.failure.ignore=true clean package"
         }

         post {
            // If Maven was able to run the tests, even if some of the test
            // failed, record the test results and archive the jar file.
            success {
              junit '**/target/surefire-reports/TEST-*.xml'
              archiveArtifacts 'target/*.jar'
            }
         }
      }
	  

	  //stage('validation')
	  //{
		//print "checking whether the jar is up and running"
		//bat "jps | find /I "demo-0.0.1-SNAPSHOT.jar"
		//bat "jps"
 	  //}	  
   }
}
