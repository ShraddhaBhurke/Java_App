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
	}
	stage('zip') {
            steps {
		bat 'rmdir /Q /S zipped_files'
	    	bat 'mkdir zipped_files'
	    	bat 'copy target\\*.jar zipped_files'
	    	bat 'copy *.sql zipped_files'
	    	echo "ZIP"
	    	zip zipFile: 'zipped_files.zip', archive: true, dir: 'zipped_files'
	    	archiveArtifacts artifacts: 'zipped_files.zip', fingerprint: true
	    	echo "END - ZIP"
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


