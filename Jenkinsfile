pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git url: 'https://github.com/ARMAAN-SAHOO/JENKINS_DEMO.git', branch: 'main'
            }
        }

        stage('Compile') {
            steps {
                bat 'javac HelloWorld.java'
            }
        }

        stage('Run Program') {
            steps {
                bat 'java HelloWorld'
            }
        }

    }
}