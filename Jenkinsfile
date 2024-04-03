pipeline {
    agent any
    
    stages {
        stage('Testing') {
            steps {
                sh 'cd webapp && sudo docker run  --rm -e SONAR_HOST_URL="http://18.224.33.125:9000" -e SONAR_LOGIN="sqa_131256bf4d478f095532f7b2bd96abf1b8f63be2"  -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectKey=lms2'
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
                    sh "curl -v -u admin:Ammu@3108 --upload-file webapp/dist-${packageJSONVersion}.zip http://18.224.33.125:8081/repository/lms/"

 

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
                    sh "curl -v -u admin:Ammu@3108 --upload-file webapp/dist-${packageJSONVersion}.zip http://18.224.33.125:8081/repository/lms-fe/"

 

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
                    sh "curl -v -u admin:Ammu@3108 --upload-file api/build-${packageJSONVersion}.zip http://18.224.33.125:8081/repository/lms-be/"

 

                }


            }
        }
        stage('Docker Build ') {
            steps{
                sh 'cd api && docker build -t srinidhi3108/api .'
                sh 'cd webapp && docker build -t srinidhi/webapp .'
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                sh 'docker push srinidhi3108/api'
                sh 'docker push srinidhi3108/webapp'
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

