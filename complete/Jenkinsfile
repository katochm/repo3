pipeline {
	agent any
	stages {
		stage('Checkout code from git repository') {
			steps {
				checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'miniproject/complete']], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'Github', url: 'https://github.com/katochm/firstrepo.git']]])
			}
			
		}
		stage('maven version') {
		    steps {
		        sh 'mvn --version'
		    }
		}
		stage('maven Build') {
			steps {
			    sh label: '', script: 'cd miniproject/complete/'
				sh label: '', script: './mvnw package && java -jar target/gs-spring-boot-docker-0.1.0.jar'
			}
			
		}
	}

}
