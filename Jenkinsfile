pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }
    environment{
       ArtifactId = readMavenPom().getArtifactId()
       Version = readMavenPom().getVersion()
       Name = readMavenPom().getName()
       GroupId = readMavenPom().getGroupId()
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

        // Stage3 : Publish the artifacts to Nexus
        stage ('Publish to Nexus'){
            steps {
                nexusArtifactUploader artifacts: [[artifactId: 'DonaldDevOpsLab', classifier: '', file: 'target/DonaldDevOpsLab-0.0.3-SNAPSHOT.war', type: 'war']], credentialsId: '3d2b504b-f147-4df3-a3d7-1986fa1cb835', groupId: 'com.donalddevopslab', nexusUrl: '172.20.10.246:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'DonaldDevOpsLab-SNAPSHOT', version: '0.0.3-SNAPSHOT'
            }
        }

        // Stage 4 : Print Some - information
        stage ('Print Environment variableas'){
            steps {
                echo "Artifact ID is '${ArtifactId}'"
                echo "Version is '${Version}'"
                echo "GroupID is '${GroupID}'"
                echo "Name is '${Name}'"
            }
        }

        // Stage 5 : Deploying
        stage ('Deploy'){
            steps {
                echo 'Deploying......'
            }
        }


    }

}