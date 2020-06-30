pipeline { 
    agent any
    stages {
        stage('Build') {
	    def mvnHome =  tool name: 'Maven', type: 'maven'   
	    bat "${mvnHome}\\bin\\mvn package"
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
	    always {
		emailext (
		to: 'shra.bhurke@gmail.com',
          	subject: "Jenkins: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
          	body: """<p>${currentBuild.currentResult}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
            	<p>Check console output at &QUOT;<a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>&QUOT;</p>""",
          	recipientProviders: [[$class: 'DevelopersRecipientProvider']]
        	)	
	    }
	}
    }
}


