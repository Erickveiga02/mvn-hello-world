pipeline {
    agent{
        label 'maven'
    }
    stages {
        stage('Build') {
            steps {
               build()
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
