pipeline {
    agent {
        node {
            label "debian && java17"
        }
    }
    
    stages {
        stage('Build') {
            steps {
                echo 'Start Build'
                sh("./mvnw clean compile test-compile")
                echo 'Finish Build'
            }
        }

        stage('Test') {
            steps {
                echo 'Start Test'
                sh("./mvnw test")
                echo 'Finish Test'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Hello Deploy 1'
                sleep(10)
                echo 'Hello Deploy 2'
            }
        }
    }

    post {
        always {
            echo 'I will always say Hello again!'
        }

        success {
            echo 'Yay, success'
        }

        failure {
            echo 'Oh no, failure'
        }

        cleanup {
            echo "Don't care success or error"
        }
    }
}
