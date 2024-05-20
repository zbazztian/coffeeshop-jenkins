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
        sh 'docker build -t coffeeshop:latest .'
        echo 'Successfully built container image.'
        
        withCredentials([
          usernamePassword(credentialsId: 'CR', usernameVariable: 'USER', passwordVariable: 'PASSWORD')
        ]){
          sh 'docker tag coffeeshop:latest 471112717199.dkr.ecr.eu-north-1.amazonaws.com/coffeeshop:latest'
          sh '/bin/bash -c "echo -n ${PASSWORD} | docker login -u ${USER} --password-stdin 471112717199.dkr.ecr.eu-north-1.amazonaws.com"'
          sh 'docker push 471112717199.dkr.ecr.eu-north-1.amazonaws.com/coffeeshop:latest'
        }
      }
    }
  }
}
