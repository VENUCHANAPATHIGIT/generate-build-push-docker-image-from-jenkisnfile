pipeline {
    agent any
    options {
    buildDiscarder(logRotator(numToKeepStr:'5'))
    disableConcurrentBuilds()
    timestamps() 
    }
    environment {
        dockerhub=credentials('venuchanapathi1998')
    }
    stages {
        stage('Starting stage') {
            steps {
                echo 'First stage of the pipeline'
            }
        }
        stage('Cleaning the cloned repo and previously loaded docker images') {
            steps {
                sh 'rm -rf ${WORKSPACE}/image-using-docker'
            }
        }
        stage('Checking docker version') {
            steps {
                sh 'docker --version'
            }
        }
        stage('Checking docker images that are currently loaded') {
            steps {
                sh 'docker images'
            }
        }
        stage('Cloning the repo') {
            steps {
                sh 'git clone https://github.com/VENUCHANAPATHIGIT/image-using-docker.git'
            }
        }
        stage('Checking the files in PWD') {
            steps {
                sh 'ls -l'
                sh 'pwd'
            }
        }
        stage('Copying the docker file to current directory') {
            steps {
                sh 'cp ${WORKSPACE}/image-using-docker/Dockerfile ${WORKSPACE}/Dockerfile'
                sh 'cp ${WORKSPACE}/image-using-docker/clock-script.py /${WORKSPACE}/clock-script.py'
            }
        }
        stage('Building docker image from docker file') {
            steps {
                sh 'docker build -f Dockerfile -t clockapp .'
            }
        }
        stage('Running the image') {
            steps {
                sh 'docker run -i --name myclock clockapp'
            }
        }
        stage('cleaning the loaded images') {
            steps {
                sh 'docker stop $(docker ps -aq)'
                sh 'docker rm $(docker ps -aq)'
                sh 'docker rmi $(docker images -q)'
            }
        }
        
        stage('Environment variables') {
            steps {
                sh 'echo ${WORKSPACE}'
            }
        }
        
        stage('last stage') {
            steps {
                echo "last stage of the pipeline"
             }
         }
    }
}
