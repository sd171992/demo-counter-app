pipeline {
    agent any

    stages{
        stage('Git Checkout'){
            steps{
                script{
                    git branch: 'main', url: 'https://github.com/sd171992/demo-counter-app.git'
                }
            }
        }
        stage('UNIT testing'){
            
            steps{
                
                script{
                    
                    sh 'mvn test'
                }
            }
        }
        stage('Integration testing'){
            
            steps{
                
                script{
                    
                    sh 'mvn verify -DskipUnitTests'
                }
            }
        }
        stage('Maven build'){
            
            steps{
                
                script{
                    
                    sh 'mvn clean install'
                }
            }
        }
        stage('upload war file to nexus'){
            steps{
                script{
                    nexusArtifactUploader artifacts: [[artifactId: 'springboot', classifier: '', file: 'target/Uber.jar', type: 'jar']], credentialsId: 'nexus-auth', groupId: 'com.example', nexusUrl: '52.90.99.153:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'demoapp-relese', version: '1.0.0'
                }
            
            }
        }
    }
}
