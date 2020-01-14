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
		stage('Setting permission to jar') {
			steps {
				sh 'sudo chmod 777 /var/lib/jenkins/workspace/pptest1/target/gs-spring-boot-docker-0.1.0.jar'
			}
		}
		stage('Docker Build') {
		    steps {
		        sh 'docker build -t katochm/firstrepo:latest .'
		    echo 'docker images is created'
		    sh 'docker images'
		    }
		}
		stage('Push artifact to Nexus Repository') {
			steps {
				echo "Pushing artifacts........"
				nexusArtifactUploader artifacts: [[artifactId: 'katochm/firstrepo', classifier: 'debug', file: '/var/lib/jenkins/workspace/pptest1/target/gs-spring-boot-docker-0.1.0.jar', type: 'jar']], credentialsId: 'nexus-creds', groupId: 'group', nexusUrl: 'localhost:8081/repository/test-repo/', nexusVersion: 'nexus3', protocol: 'http', repository: 'test-repo', version: 'Nexus/3.16.1-02 (OSS)'
				echo "..........Artifacts pushed"			
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