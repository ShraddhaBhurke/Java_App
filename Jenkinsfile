def mvnHome =  tool name: 'Maven', type: 'maven'
pipeline { 
    agent any
    stages {
        stage('Build') {
            steps {
		bat '${mvnHome}\\bin\\mvn clean package'
            }
        }
        stage('Test') {
            steps {
                bat '${mvnHome}\\bin\\mvn test'
            }
	    post {
	      always {
		emailext (
		to: 'shra.bhurke@gmail.com',
          	subject: "Jenkins: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
          	body: """<p>${currentBuild.currentResult}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
            	<p>Check console output at &QUOT;<a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>&QUOT;</p>""",
          	
        	)	
	      }
           }
	
	}
    }
}


