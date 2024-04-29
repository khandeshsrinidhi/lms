pipeline {
    agent any
    environment {
    dockerhub=credentials('docker-hub1')
    }
    
    stages {
        stage('Testing') {
            steps {
                sh 'cd webapp && sudo docker run  --rm -e SONAR_HOST_URL="http://3.137.41.205:9000" -e SONAR_LOGIN="sqa_24e7aec2a2a77081fe0d313604f9dc97cba33bba"  -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectKey=lms'
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
                    sh "curl -v -u admin:Ammu@3108 --upload-file webapp/dist-${packageJSONVersion}.zip http://3.137.41.205:8081/repository/lms/"

 

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
                    sh "curl -v -u admin:Ammu@3108 --upload-file webapp/dist-${packageJSONVersion}.zip http://3.137.41.205:8081/repository/lms-fe/"

 

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
                    sh "curl -v -u admin:Ammu@3108 --upload-file api/build-${packageJSONVersion}.zip http://3.137.41.205:8081/repository/lms-be/"

 

                }


            }
        }
       
        stage('docker building...'){
            steps{
                sh 'cd api && docker build -t srinidhi3108/api .'
                sh 'cd webapp && docker build -t srinidhi3108/webapp .'
            }
        }
        stage('Docker Login'){
            steps{
                echo 'Docker login'
                sh 'echo $dockerhub_PSW | docker login -u $dockerhub_USR --password-stdin'
            }
        }
        stage('Docker Push'){
            steps{
                echo 'docker push'
                sh 'docker push srinidhi3108/api'
                sh 'docker push srinidhi3108/webapp'
            }
        }
        stage('docker rm old files'){
            steps{
                echo 'removing old files'
                sh 'docker rmi -f srinidhi3108/api'
                sh 'docker rmi -f srinidhi3108/webapp'
            }
        }


    

  
  
       

    
        
 
    
        
            
                
                    
                        
    }
}
         





        
    

