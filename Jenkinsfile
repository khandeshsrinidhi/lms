pipeline {
    agent any
    
    stages {
        stage('Test') {
            steps {
                sh 'cd webapp && sudo docker run  --rm -e SONAR_HOST_URL="http://18.117.9.128:8080" -e SONAR_LOGIN="sqp_d3098ab39ba2dc286609770596ae1d2743bfef99"  -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectKey=lms'
            }
        }
        }
    }

