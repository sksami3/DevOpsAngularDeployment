pipeline {
    agent any

    environment {
        ANGULAR_IMAGE = 'my-angular-app'
    }

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:latest'
                    args '-u root' // Optional: Run Docker container as root
                }
            }
            steps {
                script {
                    // Install Angular CLI
                    sh 'npm install -g @angular/cli'
                    
                    // Build Angular app
                    sh 'ng build --prod'
                }
            }
        }
        stage('Test') {
            agent any
            steps {
                script {
                    // Run tests if you have any
                    echo 'Testing Angular app'
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    // Log in to Docker registry
                    withCredentials([usernamePassword(credentialsId: "${DOCKER_REGISTRY_CREDS}", passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                        sh "echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin docker.io"
                        
                        // Push Docker image
                        sh "docker push $ANGULAR_IMAGE"
                    }
                }
            }
        }
    }
    post {
        always {
            // Log out of Docker registry
            sh 'docker logout'
        }
    }
}
