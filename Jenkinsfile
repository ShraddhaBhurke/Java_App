pipeline { 
    agent any
	tools {
      // Install the Maven version configured as "M3" and add it to the path.
      maven "Maven"
      jdk "JDK"
      
   }
    stages {
        stage('Build') {
            steps {
		bat 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                bat 'mvn test'
            }
	    post {
	      always {
		emailext (
		to: 'shra.bhurke@gmail.com',
          	subject: "Jenkins: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
          	body: """<p>${currentBuild.currentResult}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
            	<p>Check console output at &QUOT;<a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>&QUOT;</p>"""
            	
          	
        	)	
	      }
           }
	
	}
    }
}


