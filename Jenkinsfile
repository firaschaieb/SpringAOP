pipeline {
    agent any
    environment{
        PATH = "$PATH:/usr/share/maven/bin"
    }

    stages {
         stage('Cloning from GitHub') {
                steps {
                    git branch: 'main', url: 'https://github.com/firaschaieb/SpringAOP.git'
                }
                
            }
          stage('MVN COMPILE') {
            steps {
               sh 'mvn compile'
            
           }
        }
        stage('MVN CLEAN') {
            steps {
               sh 'mvn clean install'
            }
        }
          stage('Test') {
            steps {
               sh 'mvn test'
            }
        }
          stage('Test package') {
            steps {
               sh 'mvn package'
            }
        }
      
      
        stage ('Scan Sonar'){
            steps {
        
    sh "mvn sonar:sonar \
  -Dsonar.projectKey=sonar1 \
  -Dsonar.host.url=http://192.168.1.23:9000 \
  -Dsonar.login=4f3d48177d195b1c3407619d318e7524c7fee3fc"

    }
        }
        stage('Nexus') {
      steps {
        sh 'mvn deploy -DskipTests'
      }
    }
       
      stage("Building Docker Image") {
                steps{
                    sh 'docker build -t firas1925/achat .'
                }
        }
        
        
           stage("Login to DockerHub") {
                steps{
                    sh 'sudo chmod 666 /var/run/docker.sock'
                   // sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u firas1925 -p fir@s99'
                }
        }
        stage("Push to DockerHub") {
                steps{
                    sh 'docker push firas1925/achat'
                }
        }
    
               stage("Docker-compose") {
                steps{
                    sh 'docker-compose up -d'
                }
        } 
    }
    
    post {
                success {
                   echo 'succes'
                }
failure {
                  echo 'failed'   
                }
             
       
    }

}
