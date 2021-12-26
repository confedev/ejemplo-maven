import groovy.json.JsonSlurperClassic

def jsonParse(def json) {
    new groovy.json.JsonSlurperClassic().parseText(json)
}
pipeline {
    agent any
    stages {

        stage("Compile Code"){
            steps {
                script {
                sh "./mvnw.cmd clean compile -e"
                }
            }
        }
        stage("Test Code"){
            steps {
                script {
                sh "./mvnw.cmd clean test -e"
                }
            }
        }
        stage("Jar Code"){
            steps {
                script {
                sh "./mvnw.cmd clean package -e"
                }
            }
        }
        stage("Run Jar"){
            steps {
                script {
                sh "./mvnw.cmd spring-boot:run "
                }
            }
        }
        stage("Testing Application"){
            steps {
                script {
                sh "curl -X GET 'http://localhost:8081/rest/mscovid/test?msg=testing'"
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
