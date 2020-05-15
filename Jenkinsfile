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
                script {
                    props = readJSON file: './release-properties.json'
                }
            }
        }
        stage('Build') {
            steps {
                echo "props.mavenComponents[0]: ${props.mavenComponents[0]}"
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                echo "props.mavenComponents[0]: ${props.mavenComponents[0]}"
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