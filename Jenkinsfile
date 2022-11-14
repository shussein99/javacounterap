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
     }    
}