pipeline {
    agent any
    
    stages {
        stage('Test') {
            steps {
                sh 'cd webapp && sudo docker run  --rm -e SONAR_HOST_URL="http://3.145.171.103:9000" -e SONAR_LOGIN="sqp_a79e911246f1adff1eeb1b1a6e18f94a44bb1455"  -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectKey=lms'
            }
        }
        }
    }

