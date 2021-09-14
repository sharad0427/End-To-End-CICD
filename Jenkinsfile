pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }
    
    stages {
        // Specify various stage with in stages

        // stage 1. Build
        stage ('Build'){
            steps {
                sh 'mvn clean install package'
            }
        }

        // Stage2 : Testing
        stage ('Test'){
            steps {
                echo ' testing......'

            }
        }
        // Stage 3: Publish artifacts to nexus
		stage ('publish') { 
		    steps {
			     nexusArtifactUploader artifacts: [[artifactId: 'VinayDevOpsLab', classifier: '', file: 'target/VinayDevOpsLab-0.0.4.war', type: 'war']], credentialsId: 'e823df7a-71e5-45c7-bf33-c068f985dae0', groupId: 'com.vinaysdevopslab', nexusUrl: '172.20.10.54:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'MyLab-SNAPSHOT', version: '0.0.4'
			}
		}	
        // Stage 4 : Deploying 
        stage ('Deploy'){
            steps {
                echo "Deploying ...."
                
            }
        }
    }

}