pipeline {
    agent any
    
    stages {
        stage('Test') {
            steps {
                sh 'cd webapp && sudo docker run  --rm -e SONAR_HOST_URL="http://3.133.157.112:9000" -e SONAR_LOGIN="sqa_e85cfb93a5bc62e30c99bf57479b0a4480d91b54"  -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectKey=lms'
            }
        }
        stage('email notifiation'){
            steps{
                emailext body: 'this is notify that build has been started',
                subject:'jenkins-notification',
                to:'khandeshsrinidhi@gmail.com',
                attachLog:true
                
            }
        }
        /*stage('Build Frontend'){
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
        stage('Releasing..'){
            steps{

            }
        }*/

        }
    }

