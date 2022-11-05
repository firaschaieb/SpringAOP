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
  -Dsonar.host.url=http://192.168.33.10:9000 \
  -Dsonar.login=b9aa7db67fb0df903d294592022f8acf7173e1a3 -DskipTests"

    }
        }
        stage('Nexus') {
      steps {
        sh 'mvn deploy -DskipTests'
      }
    }
       
    /*  stage("Building Docker Image") {
                steps{
                    sh 'docker build -t gaston2100/achat .'
                }
        }
        
        
           stage("Login to DockerHub") {
                steps{
                   // sh 'sudo chmod 666 /var/run/docker.sock'
                    sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u gaston2100 -p hinda2100@@'
                }
        }
        stage("Push to DockerHub") {
                steps{
                    sh 'docker push gaston2100/achat'
                }
        }
    
               stage("Docker-compose") {
                steps{
                    sh 'docker-compose up -d'
                }
        } */
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
