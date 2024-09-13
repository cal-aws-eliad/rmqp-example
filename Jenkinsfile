pipeline {
    agent { label 'docker' }

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub')
        GIT_REPO = 'https://github.com/cal-aws-eliad/rmqp-example.git'
        CONSUMER_IMAGE = 'calawseliad/consumer'
        PRODUCER_IMAGE = 'calawseliad/producer'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git url: "${env.GIT_REPO}"
            }
        }

        stage('Build Consumer Docker Image') {
            steps {
                script {
                    docker.build("${env.CONSUMER_IMAGE}", "./consumer")
                }
            }
        }

        stage('Build Producer Docker Image') {
            steps {
                script {
                    docker.build("${env.PRODUCER_IMAGE}", "./producer")
                }
            }
        }



        stage('Push Consumer Docker Image') {
            steps {
                script {
		    docker.image("${env.CONSUMER_IMAGE}").push('latest')
                }
            }
        }

        stage('Push Producer Docker Image') {
            steps {
                script {
                    docker.image("${env.PRODUCER_IMAGE}").push('latest')
                }
            }
        }
    }
}