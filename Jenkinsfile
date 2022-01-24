import groovy.json.JsonSlurperClassic

def jsonParse(def json) {
    new groovy.json.JsonSlurperClassic().parseText(json)
}
pipeline {
    agent any
    stages {
        
        stage("Print branch_name"){
            steps {
                script {
                    sh "echo 'branch name ${BRANCH_NAME}'"
                }
            }
        }
        
        stage("Print env"){
            steps {
                script {
                    sh 'printenv'
                }
            }
        }

        stage("Compile Code"){
            steps {
                script {
                    sh "echo 'Compile Code'"
                    sh "./mvnw clean compile -e"
                }
            }
        }
        stage("Test Code"){
            steps {
                    script {
                    sh "echo 'Test Code'"
                    sh "./mvnw clean test -e"
                }
            }
        }
        stage("Jar Code"){
            steps {
                script {
                    sh "echo 'Jar Code'"
                    sh "./mvnw clean package -e"
                }
            }
        }
        stage("Run Jar"){
            steps {
                script {
                    sh "echo 'Run Jar'"
                    sh "nohup bash mvnw spring-boot:run &"
                }
            }
        }
    }
    post {
        always {
            sh "echo 'fase always executed post'"
        }
        success {
            sh "echo 'fase success'"
        }

        failure {
            sh "echo 'fase failure'"
        }
    }
}
