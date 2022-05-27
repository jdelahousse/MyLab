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
                nexusArtifactUploader artifacts: [[
                    artifactId: "${ArtifactId}", 
                    classifier: '', 
                    file: "target/${Name}-${Version}.war", 
                    type: 'war']], 
                    credentialsId: 'e2afce96-e3d1-482d-8436-dd730495350b', 
                    groupId: "${GroupId}", 
                    nexusUrl: '172.20.10.194:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: 'VinaysDevOpsLab-SNAPSHOT', 
                    version: "${Version}"
            }
        }
        // Stage 4: Print some information
        stage ('Print Environment Variables'){
            steps {
                echo "Artifact ID is '${ArtifactId}'"
                echo "Version is '${Version}'"
                echo "Name is '${Name}'"
                echo "Group ID is '${GroupId}'"
            }
        }
        // Stage 5 : Publish the source code to Sonarqube
        stage ('Deploy'){
            steps {
                echo ' deploying......'
                }

        }

        
        
    }

}