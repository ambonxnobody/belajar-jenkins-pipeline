pipeline {
    agent none
    // agent any
    // agent {
    //     node {
    //         label "ubuntu && java17"
    //     }
    // }
    
    stages {
        stage('Prepare') {
            agent {
                node {
                    label "debian && java17"
                }
            }
            
            steps {
                echo("Start Job : ${env.JOB_NAME}")
                echo("Start Build : ${env.BUILD_NUMBER}")
                echo("Branch Name : ${env.BRANCH_NAME}")
            }
        }
        
        stage('Build') {
            agent {
                node {
                    label "ubuntu && java17"
                }
            }
            
            steps {

                script {
                    for (int i = 0; i < 10; i++) {
                        echo("Script ${i}")
                    }
                }
                
                echo 'Start Build'
                sh("./mvnw clean compile test-compile")
                echo 'Finish Build'
            }
        }

        stage('Test') {
            agent {
                node {
                    label "ubuntu && java17"
                }
            }
            
            steps {
                script {
                    def data = [
                        "firstName": "Hafid",
                        "lastName": "Dian Nurfaujan Ahat"
                    ]

                    writeJSON(file: "data.json", json: data)
                }
                
                echo 'Start Test'
                sh("./mvnw test")
                echo 'Finish Test'
            }
        }

        stage('Deploy') {
            agent {
                node {
                    label "debian && java17"
                }
            }
            
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
