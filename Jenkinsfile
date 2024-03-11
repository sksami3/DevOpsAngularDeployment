pipeline {
    agent any

    environment {
        ANGULAR_IMAGE = 'my-angular-app'
    }

    stages {
        stage('Build') {
            // agent {
            //     docker {
            //         image 'docker:dind'
            //         args '--privileged -u root'
            //     }
            // }
            steps {
                script {
                    // Set the working directory to your Angular project directory
                    //dir('path/to/your/angular/app') {
                    // Install Docker inside the Jenkins container
                    sh 'apt-get update'
                    sh 'apt-get install -y docker.io'

                    // Build Angular app
                    sh 'docker build -t my-angular-app .'
                        // Install project dependencies
                        sh 'docker build -t my-angular-app .'

                        // Build Angular app
                        sh 'docker run -d -p 8080:80 my-angular-app'
                //}
                }
            }
        }
        stage('Test') {
            agent any
            steps {
                script {
                    // Add testing steps if you have any
                    echo 'Testing Angular app'
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                        sh 'docker run -d -p 8080:80 my-angular-app'
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
