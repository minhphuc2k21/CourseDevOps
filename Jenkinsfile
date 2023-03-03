pipeline{
    
    agent any 
    //  tools { 
    //   maven 'MAVEN_HOME' 
    //   jdk 'JAVA_HOME' 
    // }
    
    stages {
        
        
        stage('sonar quaily status'){
            
            agent{
                
                docker{
            image 'maven'
                }
            }
            steps{
                
                script{
                    
                    withSonarQubeEnv(credentialsId: 'sonar-token') {
                        
                        sh 'mvn clean package sonar:sonar'
                    }
                   }
                    
                }
        }
        
       
            
            
            
            stage('Quality Gate Status'){
                
                steps{
                    
                    script{
                        
                        waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token'
                    }
                }
            }
            // stage('docker build and push to Nexus repo'){
                
            //     steps{
                    
            //         script{
                        
            //             waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token'
            //         }
            //     }
            // }
        }
        
}