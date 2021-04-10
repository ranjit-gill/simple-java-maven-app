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
      stage('Deploy') { 
      steps{
          sh 'cp target/*jar ~/myapp.jar'
          sh 'java -jar ~/myapp.jar'
        }
	 }
  }
}
