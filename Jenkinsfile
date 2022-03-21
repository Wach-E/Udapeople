pipeline {
  agent any
  stages{
    stage ("Setup-Frontend") {
      steps  { dir("frontend/") {
        nodejs('node-16.13.2'){
          sh "npm install"
          sh "sudo npm install webpack -g"
        }
      }
    }
    stage ("Test-Frontend") {
      steps  { dir("frontend/") {
        nodejs('node-16.13.2'){
          sh "npm test"
        }
      }
    }
    stage ("Scan-Frontend") {
      steps  { dir("frontend/") {
        nodejs('node-16.13.2'){
          sh "npm audit fix --audit-level=critical --force"
          sh "npm audit --audit-level=critical"
        } 
      }
    }
    stage ("Build-Frontend") {
      steps  { dir("frontend/") {
        nodejs('node-16.13.2'){
          sh "npm run build"
        } 
      }
    }
    stage ("Deploy to Dockerhub") {
      steps  { dir("frontend/") {
        withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', passwordVariable: 'PWD', usernameVariable: 'USER' )]) {
          sh "docker build -t $USER/udapeople-fe:$BUILD_NUMBER ."
          sh "echo $PWD | docker login -u $USER --password-stdin"
          sh "docker push $USER/udapeople-fe:$BUILD_NUMBER"
        }
      } 
    }
  }
}