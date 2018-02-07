pipeline {
  agent none
  stages {
    stage('Java Compile') {
      agent {
        docker {
          image 'openjdk:8'
        }
      }
      steps {
      	  sh 'javac -d . src/hello/HelloWorld.java'
      }
    }
    stage('Docker Build') {
      agent any
      steps {
        sh 'docker build -t nunojca/myrepo:latest .'
      }
    }
    stage('Docker Push') {
      agent any
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
          sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
          sh 'docker push nunojca/myrepo:latest'
        }
      }
    }
  }
}