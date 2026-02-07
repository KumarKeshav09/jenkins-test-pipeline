pipeline {
    agent any

    stages {
        stage('Checkout Info') {
            steps {
                echo "Repo is checked out"
                sh 'pwd'
                sh 'ls'
            }
        }

        stage('Groovy Demo') {
            steps {
                script {
                    def language = 'Groovy'
                    echo "Learning ${language} with Jenkins"
                }
            }
        }
    }
}
