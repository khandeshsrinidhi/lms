pipeline {
    agent any
    
    stages {
        stage('Building') {
            steps {
                sh 'cd webapp && npm install && npm run && npm build'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Deploy') {
            steps {
                sh 'scp target/myapp.war user@server:/path/to/deployment/directory'
            }
        }
    }
}
