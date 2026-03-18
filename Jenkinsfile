pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build WAR') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t mytomcatapp .'
            }
        }

        stage('Remove Old Container') {
            steps {
                sh 'docker rm -f tomcatapp || true'
            }
        }

        stage('Run New Container') {
            steps {
                sh 'docker run -d --name tomcatapp -p 8080:8080 mytomcatapp'
            }
        }
    }
}
