pipeline {
      agent any
    stages{
        stage('Build artifact'){
            steps{
               sh label: 'compile-hello-world', script: 'mvn -B -f pom.xml clean install'
            }
        }
          
        stage('Build Image'){
            steps{
               sh 'sudo docker build -t sateeshcloud06/demo:${BUILD_NUMBER} .'
            }
        }
           
        stage('Publish Image'){
            steps{
               withCredentials([string(credentialsId: 'dockerhubPwd', variable: 'dockerhubPwd')]) {
                  sh 'sudo docker login --username sateeshcloud06 --password ${dockerhubPwd}'
                }
               sh 'sudo docker push sateeshcloud06/demo:${BUILD_NUMBER}'
            }
            post{
               success{
                  sh 'sudo docker rmi -f sateeshcloud06/demo:${BUILD_NUMBER}'
               }
            }
        }

       

        

    }
}
