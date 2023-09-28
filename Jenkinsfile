pipeline{
 agent any
 tools {
  maven 'M2_HOME'
     }
stages{
  stage('Git Checkout') {
  steps {
  git 'https://github.com/mjjawad/project-banking.git'
        }
     }
  stage('Build Package'){
    steps {
           sh 'mvn clean package'
          }
       }  
   stage('Publish Html Reports'){
      steps {
           publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '/var/lib/jenkins/workspace/BankingProject/target/surefire-reports', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: '', useWrapperFileDirectly: true])       
            }
         }
   stage('Create Docker Image Of App'){
      steps{
           sh 'docker build -t jawadjk786/banking-app:1.0 .'
           }
          }  
  stage('Docker image push'){
      steps{
           withCredentials([usernamePassword(credentialsId: 'docker-hub', passwordVariable: 'docker_password', usernameVariable: 'docker_user')]) {
               
          sh 'docker login -u ${docker_user} -p ${docker_password}'
               }
           sh 'docker push jawadjk786/banking-app:1.0'
            }
        }
 
  }
}
  
