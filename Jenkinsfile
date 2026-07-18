pipeline {
  
    agent any 

    tools {
        maven 'Maven17'
    }

    stages {


        stage('user-service Build') {
            when {
                changeset "user-service/**"
            }
            steps {
                dir('user-service') {
                    sh 'mvn clean package'
                }
            }
        }

        stage('order-service Build') {
            when {
                changeset "order-service/**"
            }
            steps {
                dir('order-service') {
                    sh 'mvn clean package'
                }
            }
        }

        stage('payment-service Build') {
            when {
                changeset "payment-service/**"
            }
            steps {
                dir('payment-service') {
                    sh 'mvn clean package'
                }
            }
        }
    }

    post {

        success {
            sh 'echo "Build is Successful"'
        }

        failure {
            sh 'echo "Build is Failed"'
        }
    }
}
