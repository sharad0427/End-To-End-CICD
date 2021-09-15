pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }
    environment {
       artifactId = readMavenPom().getArtifactId()
       version = readMavenPom().getVersion()
       name = readMavenPom().getName()
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
			     nexusArtifactUploader artifacts: [[artifactId: 'VinayDevOpsLab', classifier: '', file: 'target/VinayDevOpsLab-0.0.4-SNAPSHOT.war', type: 'war']], credentialsId: 'e823df7a-71e5-45c7-bf33-c068f985dae0', groupId: 'com.vinaysdevopslab', nexusUrl: '172.20.10.54:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'MyLab-SNAPSHOT', version: '0.0.4-SNAPSHOT'
			}
		}

    // Stage 4 : Print some information
     stage ('Print Environment variables'){
                 steps {
                     echo "Artifact ID is '${ArtifactId}'"
                     echo "Version is '${Version}'"
                     echo "Name is '${Name}'"
                 }
             }
        // Stage 5 : Deploying
        stage ('Deploy'){
            steps {
                echo "Deploying ...."

            }
        }
    }

}
