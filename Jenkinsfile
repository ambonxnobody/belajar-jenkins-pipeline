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
}
