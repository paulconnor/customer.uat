pipeline{
agent any
stages {
    stage('Checkout code') {
        steps {
            checkout scm
        }
    }
    stage('Secure API - Gateway') {
        steps {
            sh 'curl -X POST -d @swagger.json http://13.237.12.95:8080/publishToProd -H "Content-Type: application/json"'
        }
    }
   /* stage('Wait for API to be deployed') {
        steps {
           timeout(5) {
               waitUntil {
                  script {
                     def r = sh script: 'wget -q http://13.237.12.95:8080/Customer -O /dev/null', returnStatus: true
                     return (r == 0);
                  }
               }
           }
        }
    } */
        stage('Enable Monitoring - Runscope') {
        steps {
            sh 'curl -X POST -d @swagger.json -H "Content-Type: application/json" http://13.237.12.95:8080/enableRunscope'     
        }
    }
    stage('Enable Management - Portal') {
        steps {
            sh 'curl -X POST -d @swagger.json http://13.237.12.95:8080/enablePAPIM -H "Content-Type: application/json"'     
        }
    }
    }
}
