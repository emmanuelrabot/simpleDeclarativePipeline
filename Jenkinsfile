pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo 'Building'
      }
    }
    stage('test') {
      when {
        expression {
          BRANCH_NAME == 'main'
        }
      }
        steps {
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
      //
    }
    success {
      //
    }
    failure {
      //
    }
  }
}
