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



pipeline {
	agent any
	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}

	stages {
		stage('build'){
			steps {
				echo 'this is build'
				sh 'mvn -v'
				sh 'docker version'
				echo "build number - $env.BUILD_NUMBER"
				echo "build ID - $env.BUILD_ID"
				echo "build TAG - $env.BUILD_TAG"
				echo "build jobs name - $env.JOB_NAME"
				echo "PATH - $PATH"
			}	
		}
		stage('compile'){
			steps {
				sh  "mvn clean compile"
			}	
		}
		stage('TEST'){
			steps {
				sh  "mvn test "
			}	
		}
		stage('Integration Test'){
			steps {
				sh "mvn failsafe:integration-test failsafe:verify"
			}	
		}
		stage('Package') {
			steps {
				sh "mvn package -DskipTests"
			}
		}
		stage('Build Docker Image') {
			steps {
				//"docker build -t in28min/currency-exchange-devops:$env.BUILD_TAG"
				script {
					dockerImage = docker.build("http://localhost:5000/currency-exchange-devops:${env.BUILD_TAG}")
				}

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