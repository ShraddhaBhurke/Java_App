pipeline { 
    agent any
    environment {
	def mvnHome =  tool name: 'Maven', type: 'maven'   
	bat "${mvnHome}\\bin\\mvn package"
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
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                bat './jenkins/scripts/deliver.sh'
            }
        }
	post {
	    success {
		emailext (
		to: 'shra.bhurke@gmail.com',
          	subject: "Successful: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
          	body: """<p>Successful: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
            	<p>Check console output at &QUOT;<a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>&QUOT;</p>""",
          	recipientProviders: [[$class: 'DevelopersRecipientProvider']]
        	)	
	    }
	}
    }
}


