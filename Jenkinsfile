pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn package'
            }
        }
        stage('Testing') {
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
            when {
                branch 'master'
		expression {
                    currentBuild.result == null || currentBuild.result == 'SUCCESS' 
                }
            }
            steps {
               sh 'mvn deploy'
            }
        }
    }
}
