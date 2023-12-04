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

           // Stage3 : Testing
        stage ('Publish to Nexus'){
            steps {
               nexusArtifactUploader artifacts: [[artifactId: 'MyTestProject', classifier: '', file: 'target/MyTestProject-0.0.3-SNAPSHOT.jar', type: 'jar']], credentialsId: 'e011c90b-880e-48ae-b427-62a512c8841a', groupId: 'MyTestProject', nexusUrl: '172.20.10.93:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'Hugh', version: '0.0.3-SNAPSHOT'

            }
        }
        
        // Stage4 : Publish the source code to Sonarqube
        stage ('Sonarqube Analysis'){
            steps {
                echo ' Source code published to Sonarqube for SCA......'
                withSonarQubeEnv('sonarqube'){ // You can override the credential to be used
                     sh 'mvn sonar:sonar'
                }

            }
        }

        
        
    }

}
