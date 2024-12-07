// node {
// 	stage('Build') {
// 		echo "Build"
// 	}
// 	stage('Test') {
// 		echo "Test"
// 	}
// 	stage('validations') {
// 		echo "Test"
// 	}
// }

environment {
		//dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$mavenHome/bin:$PATH"
	}


pipeline {
	agent any
	stages {
		stage('build'){
			steps {
				echo 'this is build'
				sh 'mvn --version'
				echo "build number - $env.BUILD_NUMBER"
				echo "build ID - $env.BUILD_ID"
				echo "build TAG - $env.BUILD_TAG"
				echo "build jobs name - $env.JOB_NAME"
				echo "PATH - $PATH"
			}	
		}
		stage('compile'){
			steps {
				echo 'this is compile'
			}	
		}	
		} 
    post {
		always {
			echo 'Im awesome. I run always'
		}
		success {
			echo 'I run when you are successful'
		}
		failure {
			echo 'I run when you fail'
		}
	}
}