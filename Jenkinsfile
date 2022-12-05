pipeline {
    agent any
    environment{
        PATH = "$PATH:/usr/share/maven/bin"
    }

    stages {
         stage('Cloning from GitHub') {
            steps {
                echo 'pulling from github';
                git branch: 'dali',
                url: 'https://github.com/firaschaieb/SpringAOP',
                credentialsId: 'b7a07fcb-55f2-462a-9a16-f41faaae0fa0';
                }
         }
               stage('MVN CLEAN') {
                        steps {
                           sh 'mvn clean '
                        }
                    }
          stage('MVN COMPILE') {
            steps {
               sh 'mvn compile'
           }
        }

          stage('mvn Test') {
            steps {
               sh 'mvn test'
            }
        }
          stage('mvn Verify') {
             steps {
               sh 'mvn verify'
          }
       }
//          stage ('Scan Sonar'){
//             steps {
//             sh "mvn sonar:sonar \
//   -Dsonar.projectKey=devops \
//   -Dsonar.host.url=http://192.168.8.101:9000 \
//   -Dsonar.login=58de8aa1109e481d57c3e7ba74ae53801df9d8be"
//   }
//         }
//         stage('Nexus') {
//           steps {
//             sh 'mvn deploy -DskipTests'
//           }
//         }
       
     stage("Building Docker Image") {
                steps{
                    sh 'docker build -t dbiradali/achatdevops .'
                }
        }


           stage("Login to DockerHub") {
                steps{
                   // sh 'sudo chmod 666 /var/run/docker.sock'
                    sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u dbiradali -p 203JMT4330'
                }
        }
        stage("Push to DockerHub") {
                steps{
                    sh 'docker push dbiradali/achatdevops'
                }
        }

//                stage("Docker-compose") {
//                 steps{
//                     sh 'docker-compose up -d'
//                 }
//         }
    }
    
//     post {
//                 success {
//                    echo 'succes'
//                 }
//                 failure {
//                   echo 'failed'
//                 }
//     }

}
