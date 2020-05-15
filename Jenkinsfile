def props

pipeline {
    agent {
        docker {
            image 'node:6-alpine'
            args '-p 3000:3000'
        }
    }
    environment {
        CI = 'true'
    }
    stages {
        stage('Read Properties') {
            steps {
                props = readJSON file: 'properties.json'
            }
        }
        stage('Build') {
            steps {
                assert props['key'] == 'value'
                assert props.key == 'value'
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                assert props['key'] == 'value'
                assert props.key == 'value'
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}