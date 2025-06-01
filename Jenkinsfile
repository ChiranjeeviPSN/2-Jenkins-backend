pipeline {
    agent {
        label 'AGENT-01'
    }

    options {
        timeout(time: 10, unit: 'MINUTES')
        disableConcurrentBuilds()
       // retry(2)
    }

    environment {
    	DEBUG = 'true'
	    appVersion = ''
    }

    stages {
        stage('Read the version') {
            steps {
		        script {
		            def packageJson = readJSON file: 'package.json'
		            appVersion = packageJson.version
		            echo "App version: ${appVersion}"
		        }
            }
        }


        stage('Install Dependencies') {
            steps {
                sh 'npm install'
                //sh 'sleep 10'
            }
        }

        stage('Docker Build') {
            steps {
                sh """
        		docker build -t test .
		        docker images
		        """
            }
       }
    }

 post {
        always{
            echo "This sections runs always"
            deleteDir()
        }
        success{
            echo "This section run when pipeline success"
        }
        failure{
            echo "This section run when pipeline failure"
        }
    }

}






