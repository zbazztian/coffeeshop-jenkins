pipeline {
  agent any
  
  stages {
    stage("run unit tests") {
      steps {
        sh 'mvn test'
        echo 'Successfully executed unit tests.'
      }
    }
    stage("build image") {
      steps {
        sh 'mvn package -DskipTests'
        echo 'Successfully compiled source code.'
        sh 'docker build .'
        echo 'Successfully built container image.'
      }
    }
  }
}
