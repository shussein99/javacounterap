pipeline{
    
agent any
    
stages{
    
    stage('Git-Checkout'){
        
        steps{
            
           script{
               
               git branch: 'main', url: 'https://github.com/shussein99/javacounterap.git'
               
                }
            
             } 
        
        }
    
    stage('UNIT Testing'){
       
        steps{
            
           script{
               
               sh 'mvn test'
               
                }
            
             } 
        }
    stage('Integration Testing'){
       
        steps{
            
           script{
               
               sh 'mvn verify -DskipUnitTests'
               
                }
            
             } 
        }
    stage('Maven Build '){
       
        steps{
            
           script{
               
               sh 'mvn clean install'
               
                }
            
             } 
        }    
    stage('Static code analysis '){
       
        steps{
            
           script{
               
               withSonarQubeEnv(credentialsId: 'sonar_api') {
                   
                  sh 'mvn clean package sonar:sonar' 
                   
                    }
               
                }
            
             } 
        }        
    stage('Quality Gate Status '){
       
        steps{
            
           script{
               
              waitForQualityGate abortPipeline: false, credentialsId: 'sonar_api'
              
                }
            
             } 
        } 
    stage('Nexus Artifact Uploader '){
       
        steps{
            
           script{
               
              nexusArtifactUploader artifacts: 
              [
                [artifactId: 'springboot', 
               classifier: '', 
               file: 'target/Uber.jar', 
               type: 'jar'
                ]
               ], 
               credentialsId: 'nexus_cred', 
               groupId: 'com.example', 
               nexusUrl: '3.16.11.38:8081', 
               nexusVersion: 'nexus3', 
               protocol: 'http', 
               repository: 'javacounterapp-release', 
               version: '1.0.0'
              
                }
            
             } 
        }       

     }    
}