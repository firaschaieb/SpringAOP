pipeline{
    agent any

    stages{


        stage('Cloning from GitHub') {
                steps {
                    git branch: 'main', url: 'https://github.com/firaschaieb/SpringAOP'
                }
                
            }
      
      stage('Clean Maven'){
            steps {
                sh 'mvn clean '
            }
            
        }
        stage('Compile Project'){
            steps {
                sh 'mvn compile  -DskipTests'
            }
            
        }
        
        
        /* stage('UNIT test'){
            steps{
                sh 'mvn test'
            }
        }*/

         stage('SonarQube Analysis'){
                steps {
                    sh """mvn sonar:sonar -DskipTests \
                            -Dsonar.language=java \
                          
                            
                    """
                }
                
            }
        
        
        
        
       stage('Nexus'){
            steps{
                sh 'mvn deploy -DskipTests'
            }
        }
     
        
      

    }
}
