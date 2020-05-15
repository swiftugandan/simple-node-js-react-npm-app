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
            script {
                props = readJSON file: './properties.json'
            }
            echo props
        }

        stage('Build') {
            steps {
                echo props.key
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                echo props.key
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