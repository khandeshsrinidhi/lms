pipeline {
    agent any
    
    stages {
        stage('Test') {
            steps {
                sh 'cd webapp && sudo docker run  --rm -e SONAR_HOST_URL="http://3.21.105.253:9000" -e SONAR_LOGIN="sqp_8f652e52d256e0b7a4747a79f6fe629756f1a616"  -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectKey=lms'
            }
        }
 /*               stage('email notifiation'){
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

