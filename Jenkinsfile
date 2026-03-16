pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git url: 'https://github.com/your-username/hello-jenkins.git', branch: 'main'
            }
        }

        stage('Compile') {
            steps {
                sh 'javac HelloWorld.java'
            }
        }

        stage('Run Program') {
            steps {
                sh 'java HelloWorld'
            }
        }

    }
}