pipeline {
    agent {
        docker {
            image 'node:latest' // Use the latest Node.js Docker image
            args '-u root' // Run the container as root to avoid permission issues
        }
    }
    environment {
        DOCKER_CREDENTIAL_ID = 'dockerhub-credentials'
        DOCKER_REPO = 'matishaikh77'
        GIT_REPO = 'https://github.com/NUCESFAST/scd-final-lab-exam-Mati-Shaikh.git'
        GIT_BRANCH = 'master'
    }
    stages {
        stage('1222-Checkout-1222') {
            steps {
                // Checkout the code from GitHub repository
                git branch: env.GIT_BRANCH, url: env.GIT_REPO
            }
        }
        stage('1222-Install Backend Dependencies-1222') {
            steps {
                // Install project dependencies for backend
                dir('Auth') {
                    sh 'npm install'
                }
                dir('Classrooms') {
                    sh 'npm install'
                }
                dir('Post') {
                    sh 'npm install'
                }
                dir('event-bus') {
                    sh 'npm install'
                }
            }
        }
        stage('1222-Install Frontend Dependencies-1222') {
            steps {
                // Install project dependencies for frontend
                dir('client') {
                    sh 'npm install'
                }
            }
        }
        stage('1222-Build Docker Images-1222') {
            parallel {
                stage('1222-Build & Push Frontend-1222') {
                    steps {
                        script {
                            dockerBuildAndPush('client', 'frontend')
                        }
                    }
                }
                stage('1222-Build & Push Auth-1222') {
                    steps {
                        script {
                            dockerBuildAndPush('Auth', 'auth')
                        }
                    }
                }
                stage('1222-Build & Push Classrooms-1222') {
                    steps {
                        script {
                            dockerBuildAndPush('Classrooms', 'classrooms')
                        }
                    }
                }
                stage('1222-Build & Push Post-1222') {
                    steps {
                        script {
                            dockerBuildAndPush('Post', 'post')
                        }
                    }
                }
                stage('1222-Build & Push Event-bus-1222') {
                    steps {
                        script {
                            dockerBuildAndPush('event-bus', 'event-bus')
                        }
                    }
                }
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}

def dockerBuildAndPush(serviceDir, serviceName) {
    def imageName = "${env.DOCKER_REPO}/${serviceName}:${env.BUILD_NUMBER}"
    dir(serviceDir) {
        docker.withRegistry('', env.DOCKER_CREDENTIAL_ID) {
            def customImage = docker.build(imageName)
            customImage.push()
        }
    }
}
