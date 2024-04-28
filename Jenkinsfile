pipeline {
        agent any
        environment {
            DOCKERHUB_CREDENTIALS=credentials('dockerhub_creadentials')
            }
        stages {
            stage('Checkout') {
                steps {
                    checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/mukulgthb/jenkinsrepository.git']])
                }
            }
            stage('Build Docker Images') {
                steps {
                    sh 'docker build -t optimusmukul/pythonapp:latest .'
                }
            }
            stage('Docker Login') {
                steps {
                    sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR -p $DOCKERHUB_CREDENTIALS_PSW'
                }
            }
            stage('Docker Image Push') {
                steps {
                    sh 'docker push optimusmukul/pythonapp:latest'
                }
            }
        }
    }