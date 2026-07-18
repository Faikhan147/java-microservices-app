pipeline {
  
    agent any 

    tools {
        maven 'Maven17'
    }

    stages {
    

        stage('Debug Git Changes') {
            steps {
                sh '''
                echo "===== CURRENT COMMIT ====="
                git rev-parse HEAD

                echo "===== PREVIOUS COMMIT ====="
                git rev-parse HEAD~1

                echo "===== CHANGED FILES ====="
                git diff --name-only HEAD~1 HEAD

                echo "===== LAST COMMIT ====="
                git show --name-only --oneline HEAD
                '''
            }
        }

        stage('Debug ChangeLog') {
            steps {
                script {
                    for (changeSet in currentBuild.changeSets) {
                        for (entry in changeSet.items) {
                            echo "Commit: ${entry.commitId}"

                            for (file in entry.affectedFiles) {
                                echo "Changed File: ${file.path}"
                            }
                        }
                    }
                }
            }
        }


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
