pipeline {
    agent any

    stages {
        stage('maven build') {
            steps {
              sh 'mvn clean package'    
            }
        }
        stage('junit report') {
            steps {
                junit allowEmptyResults: true, testResults: 'target/test-reports/*.xml'
            }
        }
        stage('record fingerprints') {
            steps {
                fingerprint 'target/*.jar'
            }
        }
        stage('archive artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false
            }
        }
    }
    post {
         always{
            cleanWs()
         }
    }
}
