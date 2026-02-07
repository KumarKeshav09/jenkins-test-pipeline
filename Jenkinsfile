pipeline {
    agent any

    parameters{
        choice (
            name: 'MODE',
            choices: ['headless', 'headed'],
            description: 'Run Playwright in headless or headed mode'
        )
    }

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

        stage('Show Mode') {
            steps {
                echo "Selected mode: ${params.MODE}"
            }
        }

        stage('Run Playwright') {
            steps {
                script {
                    if (params.MODE == 'headed') {
                        echo 'Running in HEADED mode'
                        sh 'npx playwright test --headed'
                    } else {
                        echo 'Running in HEADLESS mode'
                        sh 'npx playwright test'
                    }
                }
            }
        }
    }
}
