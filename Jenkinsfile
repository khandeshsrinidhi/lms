pipeline {
    agent any
    environment {
    dockerhub=credentials('dockerhub')
    }
    
    stages {
        stage('Testing') {
            steps {
                sh 'cd webapp && sudo docker run  --rm -e SONAR_HOST_URL="http://18.116.37.45:9000" -e SONAR_LOGIN="sqa_bed71a8278b1bde018dcc6d15fa4c7e812b241af"  -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectKey=lms1'
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
                    sh "curl -v -u admin:Ammu@3108 --upload-file webapp/dist-${packageJSONVersion}.zip http://18.116.37.45:8081/repository/lms/"

 

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
                    sh "curl -v -u admin:Ammu@3108 --upload-file webapp/dist-${packageJSONVersion}.zip http://18.116.37.45:8081/repository/lms-fe/"

 

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
                    sh "curl -v -u admin:Ammu@3108 --upload-file api/build-${packageJSONVersion}.zip http://18.116.37.45:8081/repository/lms-be/"

 

                }


            }
        }
       
        stage('docker building...'){
            steps{
                sh 'docker build -t srinidhi3108/lms .'
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
                sh 'docker push srinidhi3108/lms'
            }
        }
        stage('docker rm old files'){
            steps{
                echo 'removing old files'
                sh 'docker rmi -f srinidhi3108/lms'
            }
        }
        stage('docker run'){
            steps{
                echo 'docker running..'
                sh 'docker container run -dt --name lms-app --restart always -p 80:81 srinidhi3108/lms'
            }
        }


    

  
  
       

    
        
 
    
        
            
                
                    
                        
    }
}
         





        
    

