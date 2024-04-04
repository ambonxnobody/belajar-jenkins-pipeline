pipeline {
    agent none
    // agent any
    // agent {
    //     node {
    //         label "ubuntu && java17"
    //     }
    // }

    environment {
        AUTHOR = "Hafid Dian Nurfaujan Ahat"
        EMAIL = "ambonxnobody.15072001@gmail.com"
        WEB = "https://ambonxnobody.vercel.app/"
    }

    //  triggers {
    //    cron("*/5 * * * *")
    //    pollSCM("*/5 * * * *")
    //    upstream(upstreamProject: 'job1,job2', threshold: hudson.model.Result.SUCCESS)
    //  }

    parameters {
        string(name: "NAME", defaultValue: "Guest", description: "What is your name?")
        text(name: "DESCRIPTION", defaultValue: "Guest", description: "Tell me about you")
        booleanParam(name: "DEPLOY", defaultValue: false, description: "Need to Deploy?")
        choice(name: "SOCIAL_MEDIA", choices: ['Instagram', 'Facebook', 'Twitter'], description: "Which Social Media?")
        password(name: "SECRET", defaultValue: "", description: "Encrypt Key")
    }

    options {
        disableConcurrentBuilds()
        timeout(time: 10, unit: 'MINUTES')
    }
    
    stages {
        stage("Parameter") {
          agent {
            node {
              label "debian && java17"
            }
          }
            
          steps {
            echo "Hello ${params.NAME}"
            echo "You description is ${params.DESCRIPTION}"
            echo "Your social medis is ${params.SOCIAL_MEDIA}"
            echo "Need to deploy : ${params.DEPLOY} to deploy!"
            echo "Your secret is ${params.SECRET}"
          }
        }
        
        stage('Prepare') {
            environment {
                APP = credentials("hafid_rahasia")
            }
            agent {
                node {
                    label "debian && java17"
                }
            }
            
            steps {
                echo("Author : ${AUTHOR}")
                echo("App User : ${APP_USR}")
                // echo("App Password : ${APP_PSW}")
                sh('echo "App Password : $APP_PSW" > "rahasia.txt"')
                echo("Email : ${EMAIL}")
                echo("Web : ${WEB}")
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
            input {
                message "Can we deploy?"
                ok "Yes, of course"
                submitter "ambonxnobody"
                parameters {
                  choice(name: "TARGET_ENV", choices: ['Development', 'Staging', 'Production'], description: "Which Environment?")
                }
            }
            
            agent {
                node {
                    label "debian && java17"
                }
            }
            
            steps {
                echo("Deploy to ${TARGET_ENV}")
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
