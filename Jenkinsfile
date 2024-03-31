pipeline {
  agent {
    node {
      label "windows && java17"
    }
  }

  stages {
    stage("Hello") {
      steps {
        echo("Hello Pipeline")
      }
    }
  }

  post {
    always {
      echo "I will always say Hello again!"
    }
    success {
      echo "Yay, success"
    }
    failure {
      echo "Oh no, failure"
    }
    cleanup {
      echo "Don't care success or error"
    }
  }
}
