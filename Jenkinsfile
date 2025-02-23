pipeline {
    agent any
    stages {
        stage('init environment') {
            steps {
                echo "initializing the environment"
                sh 'export PATH=$PATH:/usr/bin'
            }
        }

        stage('SCM') {
            steps {
                echo "pulling the latest code from the repository"

                // pull the code from github repository
                git branch: 'main', url: 'https://github.com/BhaveshVP/Jenkins_Proj.git'
            }
        }

        stage('build docker image') {
            steps {
                echo "building the docker image"

                // build the docker image
                sh 'docker build -t yashpatil1902/python-server .'
            }
        }

        stage('docker login') {
            steps {
                echo "logging into docker hub"

                // login to docker hub
                sh 'echo $DOCKER_HUB_TOKEN | docker login -u yashpatil1902 --password-stdin'
            }
        }

        stage('push docker image') {
            steps {
                echo "pushing the docker image to docker hub"

                // push the docker image to docker hub
                sh 'docker push yashpatil1902/python-server'
            }
        }

        stage('remove existing docker service') {
            steps {
                echo "removing existing docker service"

                // remove the service if it already exists
                sh 'docker service rm python-server'
            }
        }

        stage('create new service') {
            steps {
                echo "creating new service"

                // create a new service
                sh 'docker service create --name python-server --replicas 2 -p 5000:5000  yashpatil1902/python-server'
            }
        }
    }
}
