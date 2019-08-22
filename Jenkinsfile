pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage ('Tests') {
            steps {
            parallel(
               'test_1': {
                    sh 'mvn test'
                },
            
                'test_2': {
                    sh 'sleep 30'
                },

                'test_3': {
                    sh 'sleep 30 && exit 1'
                }
            )}
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}
