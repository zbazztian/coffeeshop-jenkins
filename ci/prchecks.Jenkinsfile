pipeline {
  agent any
  
  stages {
    stage("build source code") {
      steps {
        sh 'mvn package -DskipTests'
      }
    }
    stage("run unit tests") {
      steps {
        sh 'mvn test'
        echo 'Unit tests succeeded!'
      }
    }
    stage("build image") {
      steps {
        sh 'docker build .'
        echo 'Container image built.'
      }
    }
  }
}
