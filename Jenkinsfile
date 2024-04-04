pipeline {
    agent none
    // agent any
    // agent {
    //     node {
    //         label "ubuntu && java17"
    //     }
    // }

    // discordSend description: "Jenkins Pipeline Build", footer: "Footer Text", link: env.BUILD_URL, result: currentBuild.currentResult, title: JOB_NAME, webhookURL: "Webhook URL

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
        // TODO: Stages in Stage Example (Sequential)
        // stage("Preparation") {
        //     agent {
        //         node {
        //           label "debian && java17"
        //         }
        //     }

        //     stages {
        //         stage("Prepare Java") {
        //             steps {
        //                 echo("Prepare Java")
        //             }
        //         }

        //         stage("Prepare Maven") {
        //             steps {
        //                 echo("Prepare Maven")
        //             }
        //         }
        //     }
        // }

        // TODO: Stages in Stage Example (Parallel)
        // stage("Preparation") {
        //    failFast true

        //     parallel {
        //         stage("Prepare Java") {
                    // agent {
                    //     node {
                    //       label "debian && java17"
                    //     }
                    // }
        //             steps {
        //                 echo("Prepare Java")
        //             }
        //         }

        //         stage("Prepare Maven") {
                    // agent {
                    //     node {
                    //       label "debian && java17"
                    //     }
                    // }
        //             steps {
        //                 echo("Prepare Maven")
        //             }
        //         }
        //     }
        // }

        // TODO: Stages in Stage Example (Matrix)
        // stage("OS Setup") {
        //   matrix {
        //     axes {
        //       axis {
        //         name "OS"
        //         values "linux", "windows", "mac"
        //       }
        //       axis {
        //         name "ARC"
        //         values "32", "64"
        //       }
        //     }
        //     excludes {
        //       exclude {
        //         axis {
        //           name "OS"
        //           values "mac"
        //         }
        //         axis {
        //           name "ARC"
        //           values "32"
        //         }
        //       }
        //     }
        //     stages {
        //       stage("OS Setup") {
        //         agent  {
        //           node {
        //             label "linux && java11"
        //           }
        //         }
        //         steps {
        //           echo("Setup ${OS} ${ARC}")
        //         }
        //       }
        //     }
        //   }
        // }
            
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

        stage("Release") {
          when {
            expression {
              return params.DEPLOY
            }
          }
          agent {
            node {
              label "debian && java17"
            }
          }
          steps {
            withCredentials([usernamePassword(
                credentialsId: "hafid_rahasia",
                usernameVariable: "USER",
                passwordVariable: "PASSWORD"
            )]) {
              sh('echo "Release it with -u $USER -p $PASSWORD" > "release.txt"')
            }
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
