pipeline {
    agent any
    
    stages {
        stage('Test') {
            steps {
                sh 'cd webapp && sudo docker run  --rm -e SONAR_HOST_URL="http://13.59.130.130:9000" -e SONAR_LOGIN="sqp_9b1f21432d53d10cf702a3cb996b6471f59bbeb7"  -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectKey=lms1'
            }
        }
        stage('email notifiation'){
            steps{
                emailtext body: 'this is notify that build has been started',
                subject:'jenkins notification',
                to:'khandeshsrinidhi@gmail.com',
                attachLog:true
                
            }
        }
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

