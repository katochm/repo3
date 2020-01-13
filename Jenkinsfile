pipeline {
	agent any
	stages {
		stage('Checkout code from git repository') {
			steps {
				checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'Github', url: 'https://github.com/katochm/firstrepo.git']]])
			}
			
		}
		stage('Maven version') {
		    steps {
		        sh 'mvn --version'
		    }
		}
		stage('Maven Build') {
		    steps {
		        sh 'mvn clean install'
		    }
		}
		stage('Docker Build') {
		    steps {
		        sh 'docker build -t katochm/firstrepo:latest .'
		    echo 'docker images is created'
		    sh 'docker images'
		    }
		}
		//stage('Push Docker Image') {
		    //steps {
		    	//withDockerRegistry(credentialsId: 'docker-hub-credentials', url: 'https://registry.hub.docker.com') {
		    	//	sh 'docker push katochm/firstrepo:latest'    
		    	//}
		        
	//	}
	      
		stage('Push Docker Image') {
		    steps {
		        sh 'docker login --username=katochm --password=Jack@1994'
		        sh 'docker push katochm/firstrepo:latest'
		    }
		}	
	}


}