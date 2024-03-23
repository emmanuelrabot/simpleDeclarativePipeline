 pipeline {
  agent any
  environment {
    CODE_CHANGES = 'true'
  }
  stages {
    stage('build') {
      when {
        expression {
          CODE_CHANGES.toBoolean()
        }
      }
      steps {
        echo "Building ${JOB_BASE_NAME}.${BUILD_ID}"
      }
    }
    stage('test') {
      when {
        expression {
          BRANCH_NAME == 'dev' || BRANCH_NAME == 'main'
        }
      }
        steps {
          echo CODE_CHANGES
          echo BRANCH_NAME
          echo 'Testing'
        }
    }
    stage('deploy') {
      steps {
        echo 'Deploying'
      }
    }
  }
  post {
    always {
      echo 'always'
    }
    success {
      echo 'success'
    }
    failure {
      echo 'failure'
    }
  }
}
