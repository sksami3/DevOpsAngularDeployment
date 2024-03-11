pipeline {
  agent any

  environment {
    ANGULAR_IMAGE = 'my-angular-app'
  }

  stages {
    stage('Build') {
      steps {
        script {
          // Install Node.js and Angular CLI
          sh 'npm install -g @angular/cli'
          
          // Build Angular app
          sh 'ng build --prod'
          
          // Build Docker image for Angular app
          sh 'docker build -t $ANGULAR_IMAGE .'
        }
      }
    }
    stage('Test') {
      steps {
        // You can include any testing commands here if you have Angular tests
        // For example: ng test
        // sh 'ng test'
      }
    }
    stage('Deploy') {
      steps {
        withCredentials([usernamePassword(credentialsId: "${DOCKER_REGISTRY_CREDS}", passwordVariable: '123456789', usernameVariable: 'sksami3')]) {
          sh "echo \$123456789 | docker login -u \$sksami3 --123456789-stdin docker.io"
          sh 'docker push $ANGULAR_IMAGE'
        }
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}
