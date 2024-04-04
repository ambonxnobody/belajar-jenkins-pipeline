pipeline {
    agent {
        node {
            label "debian && java17"
        }
    }
    
    stages {
        stage('Build') {
            steps {
                echo 'Hello Build 1'
                sleep(10)
                echo 'Hello Build 2'
            }
        }

        stage('Test') {
            steps {
                echo 'Hello Test'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Hello Deploy'
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
