pipeline{
    
    agent any 
    //  tools { 
    //   maven 'MAVEN_HOME' 
    //   jdk 'JAVA_HOME' 
    // }
    
    stages {
        
        stage('Git Checkout'){
            
            steps{
                
                script{
                    
                    git branch: 'main', url: 'https://github.com/minhphuc2k21/End-to-End-DevOps-CI-CD-Project.git'
                }
            }
        }
        stage('UNIT testing'){
            
            steps{
                
                script{
            // echo "PATH = ${PATH}"
            //         echo "M2_HOME = ${M2_HOME}"
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
        stage('Static code analysis'){
            
            steps{
                
                script{
                    
                    withSonarQubeEnv(credentialsId: 'sonar-api') {
                        
                        sh 'mvn clean package sonar:sonar'
                    }
                   }
                    
                }
            }
            stage('Quality Gate Status'){
                
                steps{
                    
                    script{
                        
                        waitForQualityGate abortPipeline: false, credentialsId: 'sonar-api'
                    }
                }
            }
        }
        
}