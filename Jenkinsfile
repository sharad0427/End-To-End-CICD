pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }
    environment {
       artifactId = readMavenPom().getArtifactId()
       version = readMavenPom().getVersion()
       groupId = readMavenPom().getGroupId()
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
         script {
           def NexusRepo = Version.endsWith("SNAPSHOT") ? "MyLab-SNAPSHOT" : "MyLab-RELEASE"
			     nexusArtifactUploader artifacts:
           [[artifactId: "${artifactId}",
           classifier: '',
           file: "target/${ArtifactId}-${Version}.war",
           type: 'war']],
           credentialsId: 'e823df7a-71e5-45c7-bf33-c068f985dae0',
           groupId: "${groupId}",
           nexusUrl: '172.20.10.54:8081',
           nexusVersion: 'nexus3',
           protocol: 'http',
           repository: "${NexusRepo}",
           version: "${version}"
        }
			}
		}

    // Stage 4 : Print some information
     stage ('Print Environment variables'){
                 steps {
                     echo "Artifact ID is '${ArtifactId}'"
                     echo "Version is '${Version}'"
                     echo "GroupID is '${GroupId}'"
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
