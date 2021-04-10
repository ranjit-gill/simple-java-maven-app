pipeline {
  agent { node { label 'linux-node-1' } }
    stages {
        
		stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        
		stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
       
	    stage('QA - Deploy') { 
		  steps{
          sh 'sudo cp target/*jar ~/myapp.jar'
          sh 'sudo java -jar ~/myapp.jar'
			}
		}
	 
		stage('Sanity check') {
          steps {
                input "Does the QA environment look ok?"
            }
        }
		
		stage('Staging - Deploy') { 
		  steps{
          sh 'sudo cp target/*jar ~/myapp.jar'
          sh 'sudo java -jar ~/myapp.jar'
			}
		}
  }
}
