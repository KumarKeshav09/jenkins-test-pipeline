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
          def cmd = "npx playwright test --reporter=html"

          if (params.MODE == 'headed') {
            cmd += " --headed"
            echo "🖥 Running in HEADED mode"
          } else {
            echo "⚡ Running in HEADLESS mode"
          }

          sh cmd
        }
      }
    }

    stage('Verify Report') {
      steps {
        sh '''
          echo "Checking playwright-report directory"
          ls -la playwright-report || true
        '''
      }
    }
  }

  post {
    always {
      echo '📊 Publishing Playwright HTML report'

      publishHTML([
        allowMissing: false,
        alwaysLinkToLastBuild: true,
        keepAll: true,
        reportDir: 'playwright-report',
        reportFiles: 'index.html',
        reportName: 'Playwright HTML Report'
      ])
    }
  }
}
