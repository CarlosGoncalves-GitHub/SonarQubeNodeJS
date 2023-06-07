
pipeline {
    agent {
		label "JenkinsSlave"
	}
    stages {
        
        stage('Code Checkout') {
            steps {
	    checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'CarlosGithub', url: 'https://github.com/CarlosGoncalves-GitHub/SonarQubeNodeJS']])
            }
        }
		stage('Code Build') {
            steps {
                echo 'Code Build'
				sh """
					ls -lart
					npm install
					npm run build
				"""
            }
        }
		stage('Test Automation') {
            steps {
                echo 'Test Automation'
				sh """
					npm run test
					npm run test:e2e
				"""
            }
        }
		stage('Code Deployment') {
            steps {
                echo 'Code Deployment'
            }
        }
}

	post {
		success {
			echo "Build is Success !!!!"
		}
		
        failure {    
			echo "Build is Failure !!!!"
        }
		always {
			emailext attachLog: true, 
                body: "$JOB_NAME - Build # $BUILD_NUMBER - $currentBuild.currentResult :\nCheck console output at $BUILD_URL to view the results.", 
                compressLog: true, subject: "$JOB_NAME - Build # $BUILD_NUMBER - $currentBuild.currentResult !", to: 'carloshmego@hotmail.com'
		}
		
    }
}
