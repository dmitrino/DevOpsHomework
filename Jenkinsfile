pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'echo "Build"'
            }
        }
        retry(2) { stage ('Tests') {

            
                parallel{
                stage('Test A') {
                        sh 'mvn test' 
                }
                stage('Test B') {
                    sh 'sleep 30'
                }

                stage('Test C') {
                    sh 'sleep 30 && exit 1'
                }
                }
         }}
        stage('Deliver') {
            steps {
                sh 'echo "OK"'
            }
        }
    }
}