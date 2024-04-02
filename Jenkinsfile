pipeline {
    agent any
    
    stages {
        stage('Testing') {
            steps {
                sh 'cd webapp && sudo docker run  --rm -e SONAR_HOST_URL="http://3.145.188.191:9000" -e SONAR_LOGIN="sqp_89115f1f4ba3f5248e153cb77faa2c8f35c5d085"  -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectKey=lms2'
            }
        }

        stage('email notification') {
            steps {
                emailext body: 'this is to notify that build job has been started',
                subject: 'jenkins-notification',
                to: 'khandeshsrinidhi@gmail.com',
                attachLog: true
            }
        }


        stage('Build Frontend'){
            steps{
                echo 'Building..'
                sh 'cd webapp && npm install && npm run build'
            }
        }
        stage('Building Backend'){
            steps{
                echo 'Building..'
                sh 'cd api && npm install && npm run build'
            }
        }
        stage('Releasing...'){
            steps{
                script{
                    echo 'releasing..'
                    def packageJSON = readJSON file: 'webapp/package.json'
                    def packageJSONVersion = packageJSON.version
                    echo "${packageJSONVersion}"
                    sh "zip webapp/dist-${packageJSONVersion}.zip -r webapp/dist"
                    sh "curl -v -u admin:Ammu@3108 --upload-file webapp/dist-${packageJSONVersion}.zip http://3.145.188.191:8081/repository/lms/"

 

                }


            }
        }
        stage('frontend Releasing...'){
            steps{
                script{
                    echo 'releasing..'
                    def packageJSON = readJSON file: 'webapp/package.json'
                    def packageJSONVersion = packageJSON.version
                    echo "${packageJSONVersion}"
                    sh "zip webapp/dist-${packageJSONVersion}.zip -r webapp/dist"
                    sh "curl -v -u admin:Ammu@3108 --upload-file webapp/dist-${packageJSONVersion}.zip http://3.145.188.191:8081/repository/lms-fe/"

 

                }


            }
        }
        stage('backend Releasing...'){
            steps{
                script{
                    echo 'releasing..'
                    def packageJSON = readJSON file: 'api/package.json'
                    def packageJSONVersion = packageJSON.version
                    echo "${packageJSONVersion}"
                    sh "zip api/build-${packageJSONVersion}.zip -r api/build"
                    sh "curl -v -u admin:Ammu@3108 --upload-file api/build-${packageJSONVersion}.zip http://3.145.188.191:8081/repository/lms-be/"

 

                }


            }
        }


        /*
        stage('deploying'){
            steps{
                script{
                    
                }
            }
        }*/


        }
    }

