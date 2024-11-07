pipeline {
    agent { label 'dev' }

    stages {
        stage('git checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Lakshman386/gctech.git'
            }
        }
        stage('maven build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('container & image remove') {
            steps {
                sh 'sudo docker rm -f cont-1'
                sh 'sudo docker rmi lakshman386/project-2:p2'
            }
        }
        stage('Docker Build & Push') {
            steps {
                script {
                   withDockerRegistry(credentialsId: 'lakshman386') {
                        sh "docker build -t lakshman386/project-2:p2 ."
                        sh "docker push lakshman386/project-2:p2"
                    }
                }
            }
        }
        stage('run') {
            steps {
                sh 'sudo docker run -d -p 8080:8080 --name cont-1 lakshman386/project-2:p2'
            }
        }
    }
}
