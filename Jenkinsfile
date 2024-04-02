pipeline {
    agent any
    
    stages {
        stage('Test') {
            steps {
                sh 'cd webapp && sudo docker run  --rm -e SONAR_HOST_URL="http://13.58.208.152:9000" -e SONAR_LOGIN="sqa_9997500a0e5e50954b73a8c57af3a06f1d8e4254"  -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectKey=lms'
            }
        }
        /*stage('email notifiation'){
            steps{
                emailtext body: 'this is notify that build has been started',
                subject:'jenkins notification',
                to:'khandeshsrinidhi@gmail.com',
                attachLog:true
                
            }
        }*/
        stage('Build Frontend'){
            steps{
                echo 'Building..'
                sh 'cd webapp && npm install && npm run build'
            }
        }
        stage('Build Backend'){
            steps{
                echo 'Building..'
                sh 'cd api && npm install && npm run build'
            }
        }

        }
    }

