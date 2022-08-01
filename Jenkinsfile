pipeline {
  agent any
  tools {
    maven 'Maven' 
  }
  stages {
    stage ('Build Maven') {
      steps {
       echo 'hello world'
       checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/sg31011991/demo-jenkins-mvn.git']]])
        sh 'mvn -Dmaven.test.failure.ignore=true clean package'
      }
    }
    stage ('Build Docker Image') {
      steps {
         script {
             sh 'docker build -t srimanta104/my-app-1.0 .'
             
         }
      }
    }
    stage ('Push Build Docker Image') {
      steps {
         script {
             withCredentials([string(credentialsId: 'srimanta104', variable: 'dockerhubpwd')]) {
             sh 'docker login -u srimanta104 -p ${dockerhubpwd}'
                     
             sh 'docker push srimanta104/my-app-1.0'
               }
             
         }
      }
    }
  }
} 
