pipeline {
  agent any

  environment {
    PATH = "/opt/homebrew/bin:${env.PATH}"
    CI = "true"
  }

  parameters {
    choice(
      name: 'MODE',
      choices: ['headless', 'headed'],
      description: 'Playwright run mode'
    )
  }

  stages {

    stage('Check Node') {
      steps {
        sh '''
          node -v
          npm -v
          npx -v
        '''
      }
    }

    stage('Install Dependencies') {
      steps {
        sh 'npm install'
      }
    }

    stage('Install Playwright Browsers') {
      steps {
        sh 'npx playwright install chromium'
      }
    }

    stage('Run Playwright Tests') {
      steps {
        script {
          def runCmd = "npx playwright test"

          if (params.MODE == 'headed') {
            runCmd += " --headed"
            echo "🚀 Running in HEADED mode"
          } else {
            echo "⚡ Running in HEADLESS mode"
          }

          sh runCmd
        }
      }
    }
  }

  post {
    always {
      echo '📊 Publishing Playwright HTML report'

      publishHTML([
        allowMissing: true,
        alwaysLinkToLastBuild: true,
        keepAll: true,
        reportDir: 'playwright-report',
        reportFiles: 'index.html',
        reportName: 'Playwright Test Report'
      ])
    }
  }
}
